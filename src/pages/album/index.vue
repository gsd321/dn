<template>
    <view>
        <!-- 专辑背景 开始 -->
        <view class="album_bg">
            <image mode="widthFix" :src="myRes.cover"></image>
            <view class="album_info">
                 <view class="album_name">
                     {{myRes.name}}
                 </view>
                 <view class="album_btn">关注专辑</view>
            </view>
        </view>
       <!--  专辑背景 结束 -->

<!-- 专辑作者 开始 -->
   <view class="album_author">
        <view class="album_author_info">
            <image mode="widthFix" :src="myRes.user.avater"></image>
            <view class="author_name">{{myRes.user.name}}</view>
        </view>
  <view class="album_author_desc">
   <text>{{myRes.desc}}</text>
      </view>
    </view>
<!-- 专辑作者 结束 -->

<!-- 列表开始 -->
<view class="album_list">
    <view class="album_item"
     v-for="(item,index) in wallpaper"
     :key="item.id"  
    >
    <go-detail :list="wallpaper" :index="index">
    <image mode="widthFix" :src="item.thumb+item.rule.replace('$<Height>',360)"></image>
    </go-detail>
    </view>

</view>
<!-- 列表结束 -->

    </view>
    

</template>

<script>
import goDetail from"@/components/goDetail"

export default{
  components: { goDetail },
    data(){
        return{
            params:{
                 limit:30,
                 order:"new",
                 skip:0,
                 first:1
            },
            id:-1,
            myRes:{},
            wallpaper:[],
            hasMore:true
        }
    },
   onLoad(options){
       console.log(options);
      this.id=options.id
    this.id="5e26b92be7bce739af7644b3"
       this.getList()
   },
  //页面触底 上拉加载下一页事件
  onReachBottom(){
      console.log("阿娇");
      if(this.hasMore){
          this.params.first=0;
          this.params.skip+=this.params.limit
          this.getList();
      }else{
          uni.showToast({
              title:"没有更多数据了",
              icon:"none"
          })
      }
  },

   methods:{
        getList(){
            this.request({
              url: `https://run.mocky.io/v3/3776415d-e52a-4921-b879-bae9848d3d9d`,
              data:this.params
            })
            .then(result=>{
                //console.log(result);
                if(Object.keys(this.myRes).length === 0){
                    console.log(result);
                      this.myRes = result.res;                
                }
        
              if(result.wallpaper.length === 0){
                  this.hasMore = false;
                   uni.showToast({
                   title:"没有更多数据了",
                   icon:"none"
               })
                  return
              }
                this.wallpaper=[...this.wallpaper,...result.wallpaper];
            
           /*      this.album=result.res.cover;
                 let myN = result.res.name;
              this.wallpaper=result.res.wallpaper;  */

                 //console.log(this.album);
            })
       }
   }
} 
</script>

<style lang="scss">
.album_bg{
    position: relative;
    .image{
   
    }
.album_info{
    position:absolute;
    width: 100%;
    left: 0;
    bottom:0;
    display: flex;
    justify-content: space-between;
    height: 80rpx;
    align-items: center;
    color: #fff;
    padding: 0 15rpx;
    .album_name{
        font-size: 40rpx;
    }
    .album_btn{
       background-color: $color;
       width: 152rpx;
       height: 60rpx;
       display: flex;
       justify-content: center;
       align-items: center;
       border-radius: 10rpx;
    }
  }
}

.album_author{
    padding: 10rpx;
    .album_author_info{
        padding: 10rpx 0;
        position: relative;
        image{
        width: 50rpx ;
        position: absolute;
        bottom: 10rpx;
        }
        .author_name{
            color: #000;
            margin-left: 60rpx;
        }
    }   
    .album_author_desc{

    }
}

.album_list{
    display: flex;
    flex-wrap: wrap;
    .album_item{
        width: 33.33%;
        border: 3rpx solid #000;
        image{

        }
    }
}

</style>