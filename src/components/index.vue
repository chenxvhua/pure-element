<template>
    <div class="content-wraper">
        <breadcrumb :current-router="$route"></breadcrumb>
        <br/><br/>
        1.<router-link :to="{ path: '/DatePicker'}"> <i class="el-icon-setting"></i>日期组件(DatePicker)</router-link><br/>
        2.<router-link :to="{ path: '/Form'}"> <i class="el-icon-setting"></i>Form表单(Form)</router-link><br/>
        3.<router-link :to="{ path: '/Pagination'}"> <i class="el-icon-setting"></i>分页组件(Pagination)</router-link><br/>
        4.<router-link :to="{ path: '/VueSelect'}"> <i class="el-icon-setting"></i>下拉分页组件(vue-select)</router-link><br/>
        5.<router-link :to="{ path: '/table'}"> <i class="el-icon-setting"></i>表格编辑(table)</router-link><br/>
        6.<router-link :to="{ path: '/tableBatch'}"> <i class="el-icon-setting"></i>表格批量编辑(table)</router-link><br/>
    </div>
</template>
<script>
    export default {
        data () {
            return {

            }
        },
        mounted (){

        },
        methods : {
            handleClick(){

            }
        }
    }
</script>
<style scoped>


</style>
