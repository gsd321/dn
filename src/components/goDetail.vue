<template>
 <view @click="handleClick">
     
     <slot></slot>
     </view>   
</template>

<script>
export default {
        props:{
            list:Array,
            index:Number
        },
      methods:{
          handleClick(){
              //1将数据缓存下拉
              getApp().globalData.imgList=this.list;
              getApp().globalData.imgindex=this.index;
              //再实现点击跳转页面
              uni.navigateTo({
                  url:"/pages/imgDetail/index"
              })
          }
      }
}
</script>

<style>

</style>