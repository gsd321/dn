<template>
  <scroll-view class="album_scroll_view" scroll-y @scrolltolower="handleToLower">
    <!-- 1自动轮播 autoplay
    2指示器 indicator-dots
    3衔接轮播 circular 
    
    4 swiper
    默认的高度 150px
    5image
    默认的宽度320px => 基本样式中 重置了100%
    默认的高度 240px
    6 计算图片的宽度和高度的比例
    7把图片的比例也写到swiper标签样式
    8swiper-item
    100%
    -->

      <!--  轮播图 开始 -->
      <view class="album_swiper">
        <swiper
        autoplay
        indicator-dots
        circular
        >
          <swiper-item
          v-for="item in banner"
          :key="item.id"
          >
            <image :src="item.thumb"></image>
          </swiper-item>
        </swiper>

      </view>
      <!-- 轮播图 结束 -->
    
        <!-- 列表开始 -->
        <view class="album_list">
          <navigator class="album_item"
          v-for="item in album"
          :key="item.id"
          :url="`/pages/album/index?id=${item.id}`"
          >
          <view class="album_img"><image mode="aspectFill" :src="item.cover"></image></view>
          <view class="album_info">
              <view class="album_name">{{item.name}}</view>
              <view class="album_desc">{{item.desc}}</view>
              <view class="album_btn"><view class="album_attention">关注</view></view>
           </view>
          </navigator>
        </view>
        <!-- 列表结束 -->
  </scroll-view>
</template>

<script>
export default {
   data(){
     return{
       params:{
         limit:30,
         order:"new",
         skip:0
       },
       //轮播图数组
       banner:[],
       //列表数组
       album:[],
       //是否还有分页数据
       hasMore:true
     }
   },
      mounted(){
         //修改页面的标题
         uni.setNavigationBarTitle({title:"专辑"})   
         this.getList();
      },
      methods:{
        getList(){
          //获取接口数据
          this.request({
            url: 'http://157.122.54.189:9088/image/v1/wallpaper/album',
            data:this.params
          })
          .then(result=>{
             if(this.banner.length===0){
              this.banner=result.res.banner;
              }

                if(result.res.album.length===0){
                  this.hasMore=false;
                   uni.showToast({
                   title:"没有更多数据了",
                   icon:"none"
          })
                  return
                }

              this.album=[...this.album,...result.res.album];
          })
        },
         /* 上拉加载-执行分页 */
         handleToLower(){
           if(this.hasMore){
             this.params.skip+=this.params.limit;
             this.getList();
           }else{
             uni.showToast({
               title:"没有数据了",
               icon:"none"
             })
           }
         }
      }
}
</script>

<style lang="scss" scoped>
.album_scroll_view{
     height: calc(100vh - 36rpx);
}


.album_swiper{
  swiper{
     height: 326.1rpx;
     image{
       height: 100%;
     }
  }
}

.album_list{
  padding: 10rpx;
  .album_item{
    padding: 10rpx 0;
    display: flex;
    border-bottom: 1px solid #ccc;
    .album_img{
      flex: 1;
      padding: 10rpx;
      image{
            width: 200rpx;
            height: 200rpx;
      }
    }
    .album_info{
      flex: 2;
      padding: 0 10rpx;
      overflow: hidden;
      .album_name{
          font-size: 30rpx;
          color: #000;
          padding: 10rpx 0;
      }
      .album_desc{
          padding: 10rpx 0;
          font-size: 24rpx;

          text-overflow: ellipsis;
          overflow: hidden;
          white-space: nowrap;
      }
      .album_btn{
        padding: 10rpx;
        display: flex;
        justify-content: flex-end;/* 靠右 */
        .album_attention{
              color: $color;
              border: 1rpx solid $color;
              padding: 10rpx;
        }
      }
    }
  }
}

</style>
