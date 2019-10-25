<template>
  <section class="container">
    <!-- 侧边栏 -->
    <el-row type="flex" justify="space-between">
      <div class="cebian-box">
      <CeBianLan class="container-left" @handleCity="handleCity" />
      </div>
      <!-- 搜索栏和渲染栏 -->
      <div class="container-right">
        <Seek @cityName="cityName" :city="city" />
        <Citylist :data="citylist" />
      </div>
    </el-row>
  </section>
</template>

<script>
import CeBianLan from "@/components/post/ceBianLan";
import Seek from "@/components/post/seek";
import Citylist from "@/components/post/citylist";
export default {
  data() {
    return {
      citylist: {},
      city: ""
    };
  },

  components: {
    CeBianLan,
    Seek,
    Citylist
  },
watch:{
    city(){
        console.log(123);
        console.log(this.city);
        
    }
},
  
  methods: {
    cityName(val) {
      this.city = val;
      this.$axios({
        url: `/posts?city=${this.city}`
      }).then(res => {
        const { ...data } = res.data;
        console.log("1", res.data);
        this.citylist = data;
      });
    },

    handleCity(city){
        this.city = city;
        // console.log(this.city);
        
        this.$axios({
        url: `/posts?city=${this.city}`
        }).then(res => {
            const { ...data } = res.data;
            this.citylist = data;
            this.city=data;
        });
    }
  },
  mounted() {
      // setTimeout(() => {
      //     this.city = this.$store.statr.post.City
      // }, 1000);
    //请求机票列表数据

    this.$axios({
      url: `/posts`
    }).then(res => {
      const { ...data } = res.data;
      console.log("1", res.data);
      this.citylist = data;
    });
  }
};
</script>

<style scoped lang="less">
.container {
  width: 1000px;
  margin: 0 auto;
  margin-top: 20px;
  .el-row {
    position: relative;
    .cebian-box{
      height: 450px;
      .container-left {
        position: absolute;
        left: 0;
        top: 0;
        width: 300px;
      }
    }
    .container-right {
      margin: 0 0 20px 300px;
    }
  }
}
</style>