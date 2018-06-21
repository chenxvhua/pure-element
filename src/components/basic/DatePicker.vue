<template>
    <router-view class="child-view"  v-if="$route.matched.length > 2">
    </router-view>
    <div class="inner-container" v-else>
        <breadcrumb :current-router="$route"></breadcrumb>
        <el-date-picker
                v-model="value1"
                type="date"
                range-separator="'至'"
                default-value="'2017-1-1'"
                placeholder="选择日期范围">
        </el-date-picker>
        <pre>
            1.日期控件
               I.
            2.属性如下：
            readonly	完全只读	boolean	—	false
            disabled	禁用	boolean	—	false
            editable	文本框可输入	boolean	—	true
            clearable	是否显示清除按钮	boolean	—	true
            size	输入框尺寸	string	large, small, mini	—
            placeholder	占位内容	string	—	—
            type	显示类型	string	year/month/date/week/ datetime/datetimerange/daterange	date
            format	时间日期格式化	string	年 yyyy，月 MM，日 dd，小时 HH，分 mm，秒 ss	yyyy-MM-dd
            align	对齐方式	string	left, center, right	left
            popper-class	DatePicker 下拉层的类名	string	下面层的外加个样式类名
            picker-options	当前时间日期选择器特有的选项参考下表	见3
            range-separator	选择范围时的分隔符	string	-	' - '  如：range-separator="'至'"
            default-value	可选，DatePicker打开时默认显示的时间	Date	可被new Date()解析   如：default-value="'2017-1-1'",在value没有值的情况下下拉层默认值


            3.picker-options值如下
                shortcuts	    设置快捷选项，需要传入  备注：{ text:"", onClick:function(){} }
                disabledDate	设置禁用状态，参数为当前日期，备注：要求返回 Boolean	Function  返回true禁止，返回false启用
                firstDayOfWeek	周起始日	Number	1 到 7	7 备注：当type为week时，表示起始位置是哪里)
                onPick	选中日期后会执行的回调，只有当 daterange 或 datetimerange 才生效	Function({ maxDate, minDate })
                   I.例如： onPick:function (obj) {
                        console.log("maxDate:", obj.maxDate)
                        console.log("minDate:", obj.minDate)
                    }
        </pre>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                value1:"",
                value6:"",
                pickerOptions:{
                    firstDayOfWeek:2
                },
                daterangeOptions:{
                    firstDayOfWeek:2,
                    onPick:function (obj) {
                        console.log("maxDate:", obj.maxDate)
                        console.log("minDate:", obj.minDate)
                    }
                },
            }
        },
        mounted(){
            var that=this;

        },
        watch: {
            ...pageCommon.pageCommonWatch.commonWatch
        },
        methods : {
            ...pageCommon.pageCommonMethod.opeMethod,//增删改查方法
            ...pageCommon.pageCommonMethod.otherMethod, //页面其他方法
        },
    }
</script>
<style scoped>

</style>
