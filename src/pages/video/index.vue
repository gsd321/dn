<template>
 
    <view>
   <view class="video_tab">
        <view class="video_tab_title">
           <view class="title_inner">
             <uni-segmented-control
              :current="current" 
              :values="items.map(v=>v.title)" 
              @clickItem="onClickItem" 
              styleType="text" 
              activeColor="#d4237a">
            </uni-segmented-control>
           </view>
           <view class="iconfont icon-sousuo">

           </view>
        </view>
        <view class="video_tab_content">
           <view v-if="current<4"><video-main></video-main></view>
           <view v-if="current===4"><video-category></video-category></view>
      </view>  
    </view>
    </view>
</template>


<script>
import {uniSegmentedControl} from "@dcloudio/uni-ui";
import videoMain from "./video-main";
import videoCategory from "./video-category"
export default {
 components:{
    videoMain,
    uniSegmentedControl,
    videoCategory
  },
  data(){
    return{
        items:[
          {title:"推荐",url:"http://service.picasso.adesk.com/v3/homepage/vertical",params:{limit:30,skip:0,order:"hot"}},
          {title:"娱乐",url:"http://service.picasso.adesk.com/v3/homepage/vertical",params:{limit:30,skip:0,order:"hot"}},
          {title:"最新",url:"http://service.picasso.adesk.com/v3/homepage/vertical",params:{limit:30,skip:0,order:"hot"}},
          {title:"热门",url:"http://service.picasso.adesk.com/v3/homepage/vertical",params:{limit:30,skip:0,order:"hot"}},
          {title:"分类",url:"http://service.picasso.adesk.com/v3/homepage/vertical",params:{limit:30,skip:0,order:"hot"}},
        ],
        current:1
    };
  },
methods:{
    onClickItem(e){
        if (this.current !== e.currentIndex){
          this.current=e.currentIndex;
        }
    }
  }
 
};
</script>

<style lang="scss">
.video_tab{
   .video_tab_title{
     position: relative;
    .title_inner{ 
      width: 55%;
      margin: 0 auto;
    }
    .icon-sousuo{
      position: absolute;
        top:50%;
      transform: translateY(-50%);
      right: 5%;
    }
   }
   .video_tab_content{

   }
}

</style>