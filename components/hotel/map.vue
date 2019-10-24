<template>
  <!-- 地图的容器 -->
  <div>
    <div id="container"></div>
    <div id="panel"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
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

<style scoped lang="less">
//地图
#container {
  width: 375px;
  height: 270px;
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
</style>