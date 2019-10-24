<template>
  <div>
    <!-- 区域部分 -->
    <div class="content-left">
      <!-- 区域部分 -->
      <div class="search-options el-row">
        <div class="option-row el-row el-row--flex">
          <div class="el-col el-col-3">区域：</div>
          <div class="el-col el-col-24 hidden-all">
            <div class="scenics-box">
              <a href="#" class="location-budget active">全部</a>
              <a
                href="#"
                class="location-budget"
                v-for="(item,index) in cities.scenics"
                :key="index"
              >{{item.name}}</a>
              <!-- <a class="location-budget">视觉艺术学院</a>
              <a class="location-budget">大成名店</a>
              <a class="location-budget">南京西站</a>-->
            </div>
            <a href="#">
              <i class="el-icon-d-arrow-right"></i>
              等43个区域
            </a>
          </div>
        </div>
        <!-- 攻略部分 -->
        <div class="option-row el-row el-row--flex">
          <div class="el-col el-col-3">攻略:</div>
          <div class="el-col el-col-24">
            北京，你想要的都能在这找到。博古通今，兼容并蓄，天下一城，如是帝都。
            景点以故宫为中心向四处辐射；地铁便宜通畅，而且覆盖绝大多数景点。
            由于早上有天安门升旗仪式，所以大多数人选择在天安门附近住宿。
          </div>
        </div>
        <div class="option-row price-row el-row el-row--flex">
          <div class="el-col el-col-3">
            均价
            <sup
              class="question-mark el-tooltip"
              aria-describedby="el-tooltip-6465"
              tabindex="0"
            >?</sup>
            :
          </div>
          <div class="el-col el-col-24">
            <div class="el-row el-row--flex">
              <div class="el-col el-col-6">
                <span class="el-tooltip" aria-describedby="el-tooltip-5166" tabindex="0">
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <span class="price-budget">¥332</span>
                </span>
              </div>
              <div class="el-col el-col-6">
                <span class="el-tooltip" aria-describedby="el-tooltip-1566" tabindex="0">
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <span class="price-budget">¥521</span>
                </span>
              </div>
              <div class="el-col el-col-6">
                <span class="el-tooltip" aria-describedby="el-tooltip-5956" tabindex="0">
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <i class="iconfont iconhuangguan"></i>
                  <span class="price-budget">¥768</span>
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cities: {
      type: Object,
      default: {},
      scenics: []
    }
  },
  mounted() {
    setTimeout(() => {
      // console.log(this.list);
    }, 3000);
  }
};
</script>

<style scoped lang='less'>
.option-row {
  

  font-size: 14px;
  color: #666;
}
.iconfont {
  color: orange;
}
.location-budget {
  margin-right: 1em;
  padding: 0 2px;
  border-radius: 4px;
  display: inline-block;
  cursor: pointer;
}
</style>