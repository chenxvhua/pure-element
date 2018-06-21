<template>
    <router-view class="child-view"  v-if="$route.matched.length > 2">
    </router-view>
    <div class="inner-container" v-else>
        <template>
            <el-select
                    v-model="value9"
                    filterable
                    placeholder="请输入关键词"
                    popper-class="mypage">
                <el-option
                        v-for="item in options4"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                </el-option>
            </el-select>
        </template>

        <pre>
              1.通过自定监听scroll事件，实现滚动加载
        </pre>
    </div>
</template>
<script>
    var sCurrent=0;
    var sRequest=false;
    export default {
        data() {
            return {
                loading:false,
                options4:[
                     {value:1,lable:"测试1"},
                     {value:2,lable:"测试2"},
                     {value:3,lable:"测试3"},
                     {value:4,lable:"测试1"},
                     {value:5,lable:"测试2"},
                     {value:6,lable:"测试3"},
                     {value:7,lable:"测试1"},
                     {value:8,lable:"测试2"},
                     {value:9,lable:"测试3"},
                     {value:10,lable:"测试1"}
                 ],
                value9:"",
            }
        },
        mounted(){
            var that=this;
            //querySelector
            var dom=document.querySelector(".mypage .el-scrollbar__wrap")
            var ulDom=document.querySelector(".mypage .el-scrollbar__wrap .el-select-dropdown__list")
            var that=this;
            dom.addEventListener("scroll",function () {
                var domH=dom.offsetHeight
                var ulH=ulDom.offsetHeight
                var domP=dom.scrollTop;
                if(!sRequest){
                    if(domP+domH>=ulH){
                        sCurrent++
                        sRequest=true
                        var customLoading=document.createElement("li")
                        customLoading.className="el-select-dropdown__item custom-loading"
                        customLoading.style.textAlign="center"
                        customLoading.innerHTML="<span>加载中...</span>"
                        ulDom.appendChild(customLoading)
                        setTimeout(function () {
                            ulDom.removeChild(customLoading)
                            sRequest=false
                            var tempArr=[]
                            for(var i=0;i<10;i++){
                                tempArr.push({value:(sCurrent*10)+i+1,lable:"测试"+(sCurrent*10)+i+1})
                            }
                            that.options4.push(...tempArr)
                        },2000)
                    }
                }
            })
        },
        watch: {

        },
        methods : {
            remoteMethod(){
               var that=this;
               that.loading=true;
               setTimeout(function () {
                   that.loading=false;
               },3000)
            }
        },
    }
</script>
<style scoped>

</style>
