<template>
    <router-view class="child-view"  v-if="$route.matched.length > 2">
    </router-view>
    <div class="inner-container" v-else>
        <template>
            <el-table
                    :data="tableData"
                    style="width: 100%">

                <el-table-column
                        prop="typeLabel"
                        label="类型"
                        width="180">
                    <template scope="scope">
                        <el-select v-model="editItem.typeValue" v-if="scope.row.isEdit"  placeholder="是否免费" clearable>
                            <el-option
                                    v-for="item in typeList"
                                    :key="item.value"
                                    :label="item.label"
                                    :value="item.value">
                            </el-option>
                        </el-select>
                        <span v-if="!scope.row.isEdit">{{scope.row.typeLabel}}</span>
                    </template>
                </el-table-column>

                <el-table-column
                        prop="date"
                        label="日期">
                    <template scope="scope">
                        <el-date-picker
                                v-model="editItem.date"
                                v-if="scope.row.isEdit"
                                type="date"
                                placeholder="选择日期">
                        </el-date-picker>
                        <span v-if="!scope.row.isEdit">{{scope.row.date}}</span>
                    </template>
                </el-table-column>
                <el-table-column
                        prop="name"
                        label="姓名"
                        width="180">
                    <template scope="scope">
                        <el-input v-model="editItem.name" v-if="scope.row.isEdit"  placeholder="请输入姓名"></el-input>
                        <span v-if="!scope.row.isEdit">{{scope.row.name}}</span>
                    </template>
                </el-table-column>

                <el-table-column
                        prop="address"
                        label="地址">
                    <template scope="scope">
                        <el-input v-model="editItem.address" v-if="scope.row.isEdit" placeholder="请输入地址"></el-input>
                        <span v-if="!scope.row.isEdit">{{scope.row.address}}</span>
                    </template>
                </el-table-column>

                <el-table-column label="操作">
                    <template scope="scope">
                        <el-button type="text" icon="edit" v-if="!scope.row.isEdit"  @click="handleEdit(scope)">编辑</el-button>
                        <el-button type="text" icon="edit" v-if="scope.row.isEdit" @click="handleOK(scope)">确定</el-button>
                        <el-button type="text" icon="edit" v-if="scope.row.isEdit" @click="handleCancel(scope)">取消</el-button>
                    </template>
                </el-table-column>

            </el-table>
        </template>
        <div>
            <el-button @click="handleSave">提交保存</el-button>
            <el-button @click="handleSave">批量</el-button>
        </div>
        <pre>
              1.因为isEdit之前没与这个key ,所有需要重新复制data中的tableData
        </pre>
    </div>
</template>
<script>
    var pureDateTime = require("puredatetime");
    export default {
        data() {
            return {
                typeList:[{
                    label:"文字1",
                    value:1
                },{
                    label:"文字2",
                    value:2
                },{
                    label:"文字3",
                    value:3
                }],
                editItem:{
                    typeValue:0,
                    date: '',
                    name: '',
                    address: ''
                },
                tableData: [{
                    typeLabel:"文字1",
                    typeValue:1,
                    date: '2016-05-02',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄'
                }, {
                    typeLabel:"文字2",
                    typeValue:2,
                    date: '2016-05-04',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1517 弄'
                }, {
                    typeLabel:"文字3",
                    typeValue:3,
                    date: '2016-05-01',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1519 弄'
                }]
            }
        },
        mounted(){

        },
        watch: {

        },
        methods : {
            handleEdit(scope){
                this.editItem.typeValue=scope.row.typeValue
                this.editItem.date=scope.row.date
                this.editItem.name=scope.row.name
                this.editItem.address=scope.row.address
                var tempArr=_.cloneDeep(this.tableData)
                var index=_.findIndex(tempArr,['isEdit', true])
                if(~index){
                    tempArr[index].isEdit=false
                }
                tempArr[scope.$index].isEdit=true
                this.tableData=tempArr
            },
            handleOK(scope){
                var typeIndex=_.findIndex(this.typeList,['value', this.editItem.typeValue])
                this.tableData[scope.$index].typeLabel=this.typeList[typeIndex].label
                this.tableData[scope.$index].typeValue=this.editItem.typeValue
                this.tableData[scope.$index].date= pureDateTime.formatDate(this.editItem.date,"yyyy-MM-dd")
                this.tableData[scope.$index].name=this.editItem.name
                this.tableData[scope.$index].address=this.editItem.address
                this.tableData[scope.$index].isEdit=false
            },
            handleCancel(scope){
                this.tableData[scope.$index].isEdit=false
            },
            handleSave(){
                 console.log(this.tableData)
            }
        },
    }
</script>
<style scoped>

</style>
