<template>
  <!-- 整个div -->
  <div class="containerall">
    <!-- 标题头部 -->
    <hoteltitle @handleCities="handleCities" />

    <!-- 中间内容区域部分 -->
    <div class="content">
      <!-- 文字内容部分 -->
      <hotelcontent :list="hotelcontent" :cities="cities" />

      <!--高德地图部分 -->
      <div class="content-right">
        <!--高德地图部分 -->
        <div>
          <!-- 地图的容器 -->
          <hotelmap />
        </div>
      </div>
    </div>

    <!-- 选择项 -->
    <hotelchoose />

    <!-- 酒店信息详情 -->
    <hotelInfo v-for="(item,index) in hotelList" :key="index" :hoteldetail="item" />
  </div>
</template>

<script>
//导入子组件
import hotelmap from "@/components/hotel/map";
import hoteltitle from "@/components/hotel/title";
import hotelchoose from "@/components/hotel/choose";
import hotelcontent from "@/components/hotel/content";
import hotelInfo from "@/components/hotel/hotelinfo";

export default {
  data() {
    return {
      start: "",
      end: "",
      hotelcontent: [],
      city: "",
      cities: {},
      //定义空数组
      hotelList: []
    };
  },

  components: {
    hotelmap,
    hoteltitle,
    hotelchoose,
    hotelcontent,
    hotelInfo
  },
  methods: {
    //从子组件中获取给父组件
    handleCities(cities) {
      // console.log(cities);
      this.cities = cities;
    },
    getHotelInfo(id) {
      this.$axios({
        url: `/hotels?&city=${id}`
      }).then(res => {
        console.log('88888888',res.data.data);
        //获取到的数据赋值
        this.hotelList = res.data.data;
      });
    }
  },
  mounted() {
    //酒店信息
    // this.$axios({
    //   url: `/cities?name=${this.city}`
    // }).then(res => {
    //   //打印数据请求
    //   console.log(res.data);
    //   const { data } = res.data;
    //   this.hotelcontent = data;
    // });
    this.getHotelInfo(74);
  },
  watch: {
    cities: {
      handler(val) {
        console.log(val);
        this.getHotelInfo(val.id);
      },
      deep: true
    }
  }
};
</script>

<style scoped lang='less'>
* {
  margin: 0;
  padding: 0;
}
//整个div
.containerall {
  width: 1000px;
  margin: 0 auto;

  .price {
    width: 98px;
    height: 42px;
    background-color: #409eff;
    border-color: #409eff;
    color: #fff;
    line-height: 1;
    white-space: nowrap;
    cursor: pointer;
    border-radius: 4px;
  }
  .gonglue {
    height: 75px;
    display: flex;
  }

  .quyu {
    height: 150px;

    display: flex;
  }

  .content {
    display: flex;
    .content-left {
      flex: 2;
    }
    .content-right {
      flex: 1;
    }
  }
}
</style>