<template>
  <div>
    <!-- 标题头 -->
    <div class="title">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/' }">酒店</el-breadcrumb-item>
        <el-breadcrumb-item>广州市酒店预订</el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <!-- 搜索栏 -->
    <div class="search">
      <!-- 搜索框左 -->
      <el-select multiple filterable remote reserve-keyword placeholder="请输入关键词">
        <el-option></el-option>
      </el-select>
      <!-- 开始日期到结束日期 -->

      <el-date-picker
        v-model="value1"
        type="daterange"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
      ></el-date-picker>

      <!-- 人数选择框 -->

      <el-select placeholder="请选择活动区域">
        <el-option label="区域一" value="shanghai"></el-option>
        <el-option label="区域二" value="beijing"></el-option>
      </el-select>

      <el-button type="primary">查看价格</el-button>
    </div>

    <div class="content">
      <div class="content-left">
        <!-- 区域部分 -->
        <div class="quyu">
          <span>区域:</span>
          <div class="quanbu">
            <span>全部</span>
            <el-button icon="el-icon-arrow-down"></el-button>
            <span>等0个区域</span>
          </div>
        </div>
        <!-- 攻略部分 -->
        <div class="gonglue">
          <span>攻略:</span>
          <span>北京，你想要的都能在这找到。博古通今，兼容并蓄，天下一城，如是帝都。 景点以故宫为中心向四处辐射；地铁便宜通畅，而且覆盖绝大多数景点。 由于早上有天安门升旗仪式，所以大多数人选择在天安门附近住宿。</span>
        </div>
        <!-- 均价 -->
        <div>
          <span>均价:</span>
          <i class="question-mark el-tooltip"></i>
          <i class="iconfont iconhuangguan"></i>
          <i class="iconfont iconhuangguan"></i>
          <i class="iconfont iconhuangguan"></i>
          <span>￥332</span>

          <span>&nbsp;&nbsp;&nbsp;&nbsp;</span>
          <i class="question-mark el-tooltip"></i>
          <i class="iconfont iconhuangguan"></i>
          <i class="iconfont iconhuangguan"></i>
          <i class="iconfont iconhuangguan"></i>
          <span>￥521</span>

          <span>&nbsp;&nbsp;&nbsp;&nbsp;</span>
          <i class="question-mark el-tooltip"></i>
          <i class="iconfont iconhuangguan"></i>
          <i class="iconfont iconhuangguan"></i>
          <i class="iconfont iconhuangguan"></i>
          <span>￥799</span>
        </div>
      </div>

      <div class="content-right">
        <!--高德地图部分 -->
        <div style="padding:50px;">
          <!-- <h3>高德地图</h3>

          <el-row style="margin-bottom:20px;">
            <el-col :span="5">
              <el-input placeholder="出发地点" v-model="start"></el-input>
            </el-col>
            <el-col :span="5">
              <el-input placeholder="到达地点" v-model="end"></el-input>
            </el-col>
            <el-button :span="2" @click="handleSearch">搜索</el-button>
          </el-row>-->

          <!-- 地图的容器 -->
          <div id="container"></div>
          <div id="panel"></div>
        </div>
      </div>
    </div>

    <!-- 选择项 -->
    <div class="xuanze">
      <el-col>
        <div class="block">
          <span class="demonstration">价格</span>
          <el-slider v-model="value1"></el-slider>
        </div>
      </el-col>
      <!-- 等级 -->
      <el-col class="dengji">
        <span class="demonstration">住宿等级</span>
        <el-dropdown>
          <span class="el-dropdown-link">
            不限
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item icon="el-icon-plus">1</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-plus">2</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>

      <!-- 类型 -->
      <el-col class="leixing">
        <span class="demonstration">住宿类型</span>
        <el-dropdown>
          <span class="el-dropdown-link">
            不限
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item icon="el-icon-plus">1</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-plus">2</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>
      <!-- 设施 -->
      <el-col class="leixing">
        <span class="demonstration">设施</span>
        <el-dropdown>
          <span class="el-dropdown-link">
            不限
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item icon="el-icon-plus">1</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-plus">2</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      start: "",
      end: "",

      value1: ""
    };
  },

  methods: {
    handleSearch() {
      this.map();
    },
    map() {
      // 地图对象
      var map = new AMap.Map("container", {
        zoom: 11 //级别
        //center: [113.3245904, 23.1066805]//中心点坐标
      });

      // 点标记
      // var marker1 = new AMap.Marker({
      //   content: `<div style="width:20px; height:20px; border-radius: 50px; background:red; color:#fff; text-align:center; line-height: 20px;">99</div>`,
      //   position:[113.3245904, 23.1066805]//位置
      // })
      // var marker2 = new AMap.Marker({
      //   position:[113.3345904, 23.1266805]//位置
      // })
      // var markerList = [marker1, marker2];
      // map.add(markerList);//添加到地图

      // 异步加载插件
      AMap.plugin(["AMap.ToolBar", "AMap.Driving"], () => {
        //异步加载插件
        var toolbar = new AMap.ToolBar();
        map.addControl(toolbar);

        // // 驾车路线的插件
        // var driving = new AMap.Driving({
        //   map: map,
        //   panel: "panel",
        //   policy: AMap.DrivingPolicy.LEAST_TIME
        // }); //驾车路线规划

        var points = [{ keyword: this.start }, { keyword: this.end }];

        driving.search(points, function(status, result) {});
      });
    }
  },

  mounted() {
    // 整个页面加载完毕之后执行
    window.onLoad = () => {
      this.map();
    };

    // 地图的连接
    var url =
      "https://webapi.amap.com/maps?v=1.4.15&key=e3c936027dd8c0a7d48d60c4db2e827e&callback=onLoad";
    var jsapi = document.createElement("script");
    jsapi.charset = "utf-8";
    jsapi.src = url;
    document.head.appendChild(jsapi);
  }
};
</script>

<style scoped lang='less'>
#container {
  width: 250px;
  height: 250px;
}
#panel {
  position: fixed;
  background-color: white;
  max-height: 90%;
  overflow-y: auto;
  top: 10px;
  right: 10px;
  width: 280px;
}
#panel .amap-call {
  background-color: #009cf9;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}
#panel .amap-lib-driving {
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  overflow: hidden;
}

.title {
  height: 50px;
  line-height: 50px;
  display: flex;
  align-items: center;
}
.quyu {
  height: 150px;

  display: flex;
}
.gonglue {
  height: 75px;
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
.xuanze {
  display: flex;
  height: 108px;
}
</style>