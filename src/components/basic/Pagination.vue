<template>
    <router-view class="child-view"  v-if="$route.matched.length > 2">
    </router-view>
    <div class="inner-container" v-else>
        <breadcrumb :current-router="$route"></breadcrumb>

        <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[10, 20, 30, 40, 50]"
                :page-size="pageSize"
                layout="total, sizes, prev, pager, next, jumper"
                :total="total">
        </el-pagination>



        <el-button type="primary" @click="handleSearch">显示</el-button>
        <pre>
            1.绑定值不会自动更新，需要在事件回调里面更新
            2.值改变，才会触发更新

        </pre>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                currentPage4: 1,
                pageSize:10,
                total:50,
            }
        },
        mounted(){
            var that=this;

        },
        watch: {
            ...pageCommon.pageCommonWatch.commonWatch
        },
        methods : {
            handleSizeChange(val) {
                this.pageSize=val;
                console.log(`每页 ${val} 条`);
            },
            handleCurrentChange(val) {
                this.currentPage4=val;
                console.log(`当前页: ${val}`);
            },
            handleSearch(){
                this.currentPage4=1;
                console.log( this.currentPage4)
            }
        },
    }
</script>
<style scoped>

</style>
