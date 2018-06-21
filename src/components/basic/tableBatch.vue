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
                        <el-select v-model="tableData[scope.$index].typeValue" v-if="isEdit"  placeholder="是否免费" clearable>
                            <el-option
                                    v-for="item in typeList"
                                    :key="item.value"
                                    :label="item.label"
                                    :value="item.value">
                            </el-option>
                        </el-select>
                        <span v-if="!isEdit">{{handleShowTypeLabel(scope.row.typeValue)}}</span>
                    </template>
                </el-table-column>

                <el-table-column
                        prop="date"
                        label="日期">
                    <template scope="scope">
                        <el-date-picker
                                v-model="tableData[scope.$index].date"
                                v-if="isEdit"
                                type="date"
                                placeholder="选择日期">
                        </el-date-picker>
                        <span v-if="!isEdit">{{handleFormatDateTime(scope.row.date,"yyyy-MM-dd")}}</span>
                    </template>
                </el-table-column>

                <el-table-column
                        prop="name"
                        label="姓名"
                        width="180">
                    <template scope="scope">
                        <el-input v-model="tableData[scope.$index].name" v-if="isEdit"  placeholder="请输入姓名"></el-input>
                        <span v-if="!isEdit">{{scope.row.name}}</span>
                    </template>
                </el-table-column>

                <el-table-column
                        prop="address"
                        label="地址">
                    <template scope="scope">
                        <el-input v-model="tableData[scope.$index].address" v-if="isEdit" placeholder="请输入地址"></el-input>
                        <span v-if="!isEdit">{{scope.row.address}}</span>
                    </template>
                </el-table-column>
            </el-table>
        </template>
        <div>
            <el-button @click="handleSave">提交保存</el-button>
            <el-button @click="handleBatch">批量编辑</el-button>
        </div>
        <pre>
              1.通过自定监听scroll事件，实现滚动加载
        </pre>
    </div>
</template>
<script>

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
                isEdit:false,
                tableData: []
            }
        },
        mounted(){
            var that=this;
            setTimeout(function () {
                that.tableData=[{
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
            },3000)
        },
        watch: {

        },
        methods : {
            ...pageCommon.pageCommonMethod.opeMethod,//增删改查方法
            ...pageCommon.pageCommonMethod.otherMethod, //页面其他方法
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
                this.tableData[scope.$index].date= this.handleFormatDateTime(this.editItem.date,"yyyy-MM-dd")
                this.tableData[scope.$index].name=this.editItem.name
                this.tableData[scope.$index].address=this.editItem.address
                this.tableData[scope.$index].isEdit=false
            },
            handleCancel(scope){
                this.tableData[scope.$index].isEdit=false
            },
            handleSave(){
                console.log(this.tableData)
            },
            handleBatch(){
                this.isEdit=this.isEdit?this.isEdit=false:this.isEdit=true;
            },
            handleShowTypeLabel(typeValue){
                var typeIndex=_.findIndex(this.typeList,['value', typeValue])
                return this.typeList[typeIndex].label
            }
        },
    }
</script>
<style scoped>

</style>
