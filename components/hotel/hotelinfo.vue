<template>
  <div >
    <nuxt-link :to="`/hotel/details?id=${hoteldetail.id}`">
    <div class="totle">
    <div class="hotel_img">
      <img class="img" :src="`${hoteldetail.photos}`" alt />
    </div>

    <div class="hailai">
      <h3>{{ hoteldetail.name }}</h3>
      <p>
        <span>{{hoteldetail.alias}}</span>
        <i  style="color:orange"   class="iconfont iconhuangguan"></i>
        <i  style="color:orange"  class="iconfont iconhuangguan"></i>
        <i  style="color:orange"  class="iconfont iconhuangguan"></i>
        <span>{{hoteldetail.hoteltype.name}}</span>
      </p>

      <p>
        <span>
          <el-rate
            v-model="stars"
            disabled
            show-score
            text-color="#ff9900"
            
          ></el-rate>
        </span>
        <span>{{hoteldetail.stars}}分</span>
        <span>27条评价</span>
        <span>23篇游记</span>
      </p>
      <p>{{hoteldetail.address}}</p>
    </div>

    <div class="anniut">
      <div class="anniu" v-for="(item,index) in hoteldetail.products" :key="index">
        <span>{{item.name}}</span>
        <span style="color:orange">￥{{item.price}}起 ></span>
      </div>
    </div>
    </div>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  data(){
    return{
      stars:3.7,
    }
  },
  props: ["hoteldetail"],

  methods:{
    
  }
  
  
};

</script>

<style scoped lang="less">
.totle {
  display: flex;
  border-bottom: 1px solid #eee;
  padding: 20px 0px;
}
.hotel_img {
  flex: 8;
  img {
    width: 322px;
    height: 212px;
  }
}
.hailai {
  flex: 10;
  margin-left: 10px;
  h3 {
    font-size: 24px;
  }
  span {
    color: #999;
    height: 30px;
    line-height: 30px;
    width: 40px;
    font-size: 14px;
  }
}
.anniut {
  flex: 6;
  margin-left: 20px;
  .anniu {
   
    border-bottom: 1px solid #eee;
    height: 50px;
    width: 240px;
    line-height: 50px;
    display: flex;
    justify-content: space-between;
    margin-right: 20px;
  }
}
</style>