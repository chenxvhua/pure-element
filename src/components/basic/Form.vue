<template>
    <router-view class="child-view"  v-if="$route.matched.length > 2">
    </router-view>
    <div class="inner-container" v-else>
        <breadcrumb :current-router="$route"></breadcrumb>
        <el-dialog title="收货地址" :visible.sync="dialogTableVisible">
            <el-form :model="ruleForm2" :rules="rules2" ref="ruleForm2" label-width="100px" class="demo-ruleForm">
                <el-form-item label="年龄" prop="age">
                    <el-input v-model.number="ruleForm2.age"></el-input>
                </el-form-item>
                <el-form-item label="数字" prop="num" v-if="numVisible">
                    <el-input v-model.number="ruleForm2.num"></el-input>
                </el-form-item>

                <el-form-item label="域名" prop="domain" :rules="numVisible?{ required: true, message: '域名不能为空', trigger: 'blur'}:{}">
                    <el-input v-model="ruleForm2.domain"></el-input>
                </el-form-item>

                <el-form-item label="下拉" prop="dicType">
                    <el-select v-model="ruleForm2.dicType" placeholder="请选择" clearable>
                        <el-option
                                v-for="item in options"
                                :key="item.value"
                                :label="item.label"
                                :value="item.value">
                        </el-option>
                    </el-select>
                </el-form-item>


                <el-form-item>
                    <el-button type="primary" @click="submitForm('ruleForm2')">提交</el-button>
                    <el-button @click="resetForm('ruleForm2')">重置</el-button>
                    <el-button @click="numVisible?numVisible=false:numVisible=true">动态验证</el-button>
                </el-form-item>
            </el-form>
        </el-dialog>
        <el-button type="primary" @click="dialogTableVisible=true">显示</el-button>
        <el-button @click="dialogTableVisible=false">隐藏</el-button>

        <pre>
        1.this.$refs[formName].resetFields()会重置表单到之前的初始值
        2.支持动态验证，但是prop一定要有,即使在规则里面没有配置
        3.下拉框验证，默认type="string",如果type="string" 那么初始化值和数组中的value值必须都是string,其他类型一样
       </pre>
    </div>
</template>
<script>
    export default {
        data() {
            var checkAge = (rule, value, callback) => {
                if (!value) {
                    return callback(new Error('年龄不能为空'));
                }
                setTimeout(() => {
                    if (!Number.isInteger(value)) {
                        callback(new Error('请输入数字值'));
                    } else {
                        if (value < 18) {
                            callback(new Error('必须年满18岁'));
                        } else {
                            callback();
                        }
                    }
                }, 1000);
            };

            return {
                options:[{
                    value:"1",
                    lable:"文字1"
                },{
                    value:"2",
                    lable:"文字2"
                }],
                dialogTableVisible:true,
                numVisible:false,
                ruleForm2: {
                    age: '',
                    domain:"",
                    dicType:2
                },
                rules2: {
                    age: [
                        { validator: checkAge, trigger: 'blur' }
                    ],
                    num: [
                        { required: true, message: '请输入数字', trigger: 'blur' },
                    ],
                    dicType: [
                        { required: true, message: '请选择类型', type:"string",trigger: 'blur' },
                    ],
                }
            };
        },
        mounted(){
            var that=this;
            setInterval(function () {
                console.log(that.ruleForm2.age);
            },1000)
        },
        watch: {
            ...pageCommon.pageCommonWatch.commonWatch
        },
        methods : {
            ...pageCommon.pageCommonMethod.opeMethod,//增删改查方法
            ...pageCommon.pageCommonMethod.otherMethod, //页面其他方法
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        alert('submit!');
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            }
        },
    }
</script>
<style scoped>

</style>
