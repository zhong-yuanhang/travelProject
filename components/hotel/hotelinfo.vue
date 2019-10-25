<template>
  <div class="totle">
    <div class="hotel_img">
      <img
        class="img"
        :src="`${hoteldetail.photos}`"
        alt
      />
    </div>

    <div class="hailai">
      <h3>{{ hoteldetail.name }}</h3>
      <p>
        <span>{{hoteldetail.alias}}</span>
        <span>{{hoteldetail.hoteltype.name}}</span>
      </p>

      <p>
        <span>星星3.5分</span>
        <span>27条评价</span>
        <span>23篇游记</span>
      </p>
      <p>{{hoteldetail.address}}</p>
    </div>

    <div class="anniut">
      <div class="anniu" v-for="(item,index) in hoteldetail.products" :key="index">
        <span>{{item.name}}</span>
        <span>￥{{item.price}}起 ></span>
      </div>


    </div>
  </div>
</template>

<script>
export default {
  props: ["hoteldetail"]
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
  img{
    width: 322px;
    height: 212px;
  }
}
.hailai {
  flex: 10;
  margin-left: 10px;
  h3{
    font-size: 24px;
  }
  span{
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
    color: orange;
    border-bottom: 1px solid #eee;
    height:  50px;
    width: 240px;
    line-height: 50px;
    display: flex;
    justify-content: space-between;
    margin-right: 20px;
  }
}
</style>