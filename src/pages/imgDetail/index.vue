<template>
   
    <view>
        <!-- 用户信息 开始 -->
        <view class="user_info">
             <view class="user_info"><image :src="imgDetail.user.avatar"></image></view>
             <view class="user_desc">
                   <view class="user_name">{{imgDetail.user.name}}</view>
                    <view class="user_time">{{imgDetail.user.name}}</view>
             </view>
        </view>
        <!-- 用户信息 结束 -->
    </view>
</template>

<script>
export default {
    data(){
        return{
            //图片信息对象 包含着用户头像
            imgDetail:{}
        }
    },
    onLoad(){
        //console.log(getApp().globalData);
        const {imgList,imgIndex}=getApp().globalData;
        this.imgDetail=imgList[imgIndex];
    }
}
</script>

<style>

</style>