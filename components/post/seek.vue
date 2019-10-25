<template>
  <el-row class="demo-autocomplete">
    <el-col class="seek-nav">
      <el-autocomplete
        class="inline-input"
        v-model="city"
        :fetch-suggestions="querySearch"
        placeholder="请输入想去的地方，比如:'广州'"
        :trigger-on-focus="false"
      ></el-autocomplete>
      <i class="el-icon-search seek-button" @click="handleSelect(city)"></i>
    </el-col>
    <div class="seek-tuiJian">
      <span>推荐:</span>
      <a href="#" @click="guangZhou">广州</a>
      <a href="#" @click="shangHai">上海</a>
      <a href="#" @click="beiJing">北京</a>
    </div>
  </el-row>
</template>

<script>
export default {
  data() {
    return {
      restaurants: [],
      city: ""
    };
  },

  

  mounted() {
      console.log(123);
      
  },

  methods: {
    querySearch(queryString, cb) {
      var restaurants = this.restaurants;
      var results = queryString
        ? restaurants.filter(this.createFilter(queryString))
        : restaurants;
      // 调用 callback 返回建议列表的数据
      cb(results);
    },
    createFilter(queryString) {
      return restaurant => {
        return (
          restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0
        );
      };
    },
    loadAll() {
      return [
        { value: "三全鲜食（北新泾店）", address: "长宁区新渔路144号" },
        {
          value: "Hot honey 首尔炸鸡（仙霞路）",
          address: "上海市长宁区淞虹路661号"
        }
      ];
    },
    handleSelect(city) {
      this.city = city;
    //   console.log(this.city);
      this.$emit("cityName", this.city);
    },
    guangZhou() {
      this.city = "广州";
      this.$emit("cityName", this.city);
    },
    shangHai(value) {
      this.city = "上海";
      this.$emit("cityName", this.city);
    },
    beiJing() {
      this.city = "北京";
      this.$emit("cityName", this.city);
    },
    tiJiao() {}
  },
  mounted() {
    this.restaurants = this.loadAll();
  }
};
</script>
<style scoped lang="less">
.seek-nav {
  position: relative;
  .inline-input {
    border: 3px solid #ffa500;
    width: 700px;
    height: 40px;
  }
  .seek-button {
    position: absolute;
    top: 10px;
    right: 15px;
    font-size: 24px;
    color: #ffa500;
    font-weight: 700;
  }
}
.seek-tuiJian {
  color: #777;
  font-size: 12px;
  margin: 53px 0 0 0;
  a {
    margin: 3px;
  }
  a:hover {
    text-decoration: underline;
    color: #ffa500;
  }
}
</style>