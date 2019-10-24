<template>
  <div>
    <!-- 标题头 -->
    <div class="title">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/' }">酒店</el-breadcrumb-item>
        <el-breadcrumb-item>{{search}}酒店预订</el-breadcrumb-item>
      </el-breadcrumb>
    </div>

    <!-- 搜索栏 -->
    <div class="el-form hotel-search-bar el-form--inline">
      <!-- 搜索框左 -->

      <el-autocomplete
        class="inline-input"
        v-model="search"
        :fetch-suggestions="querySearch"
        placeholder="请输入内容"
        :trigger-on-focus="false"
        @select="handleSelect"
      ></el-autocomplete>

      <!-- 开始日期到结束日期 -->

      <el-date-picker
        v-model="valuedata"
        type="daterange"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
      ></el-date-picker>

      <!-- 人数选择框 -->
      <div class="el-form-item__content">
        <div>
          <!--           <el-button @click="isShow=!isShow" class="person_btn">
            <span ref="person">{{person}}</span>
          </el-button>-->
          <el-input
            placeholder="请输入内容"
            @click.native="isShow=!isShow"
            readonly="readonly"
            v-model="inputs"
            clearable
          ></el-input>
          <span>
            <i class="el-input__icon iconfont iconuser"></i>
          </span>
        </div>

        <!-- 下拉选择人数 -->
        <div class="xiala" v-if="isShow">
          <div class="meijian">
            <span>每间</span>

            <el-select v-model="adultInput" class="adult_input">
              <el-option
                v-for="(item,index) in [1,2,3,4]"
                :key="index"
                :label="`${item}成人`"
                :value="item"
              ></el-option>
            </el-select>
            <!-- 儿童 -->
            <el-select v-model="ertong" class="adult_input">
              <el-option
                v-for="(item,index) in [0,1,2,3,4]"
                :key="index"
                :label="`${item}儿童`"
                :value="item"
              ></el-option>
            </el-select>
          </div>
          <el-button
            size="small"
            style="float:right;margin-top:10px"
            type="primary"
            @click="queding"
          >确定</el-button>
        </div>
      </div>
      <el-button type="primary" @click="lookprice">查看价格</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //定义空对象
      cities: {},
      search: "南京市",
      //取反显示
      isShow: false,
      valuedata: null,
      adultInput: 2,
      ertong: 0,
      inputs: "",
      cityName: ""
    };
    //标题
    props: ["biaoti"];
  },
  methods: {
    //点击事件确定获取
    queding() {
      console.log(this.adultInput);
      const str = `${this.adultInput}成人${this.ertong}儿童`;
      this.inputs = str;
    },
    //查看价格
    lookprice() {
      console.log(666);
    },
    getSelectList(value, cb) {
      this.$axios({
        url: `/cities?name=` + value
      }).then(res => {
        //打印数据请求
        console.log(res.data, "2222222");

        cb && cb(res.data.data);
      });
    },
    // 当输入文字搜索的时候触发
    querySearch(value, cb) {
      console.log(value, "5555");

      this.getSelectList(value, data => {
        const newData = data.map(v => {
          v.value = v.name;
          return v;
        });
        cb && cb(newData);
      });
    },

    // 下拉框选择后触发
    handleSelect(item) {
      this.cities = item;
      console.log(item, 99999);

      //把输入框输入的item的值传递给父组件，通过$emit
      this.$emit("handleCities", item);
    },

    handlecity(cityName) {
      // this.cityName = cityName;
      // console.log(cityName);
    }
  },
  mounted() {
    this.getSelectList(this.search, data => this.handleSelect(data[0]));
  }
};
</script>

<style scoped lang='less'>
.title {
  height: 50px;
  line-height: 50px;
  display: flex;
  align-items: center;
}
.el-form {
  margin-bottom: 20px;
}

.el-form-item__content {
  position: relative;

  .xiala {
    position: absolute;
    width: 314px;
    height: 110px;
    padding: 12px;
    margin-top: 12px;
    color: #606266;
    background-color: #fff;
    z-index: 999;
    border-radius: 10px;
    right: 0;
    box-shadow: -3px 3px 5px rgba(207, 207, 207, 0.5);
  }
}
.meijian {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #eee;
  height: 60px;
}
.el-dropdown-link {
  border: 1px solid #eee;
  width: 92px;
  height: 28px;
}
.person_btn {
  box-sizing: border-box;
  text-align: left;
  padding-left: 12px;
  width: 217px;
  height: 40px;
  span {
    color: rgb(185, 185, 185);
  }
}
.iconuser {
  position: absolute;
  top: 0px;
  right: 5px;
}

.adult_input {
  box-sizing: border-box;
  font-size: 14px;
  padding-left: 15px;
  width: 120px;
  height: 28px;
}
</style>