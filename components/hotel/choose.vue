<template>
  <div>
    <div class="xuanze">
      <el-col>
        <div class="block">
          <span class="demonstration">价格</span>
          <span class="fudu">0--4000</span>
          <el-slider v-model="valueed" :max="4000"></el-slider>
        </div>
      </el-col>
      <!-- 等级 -->
      <el-col class="dengji">
        <p class="demonstration">住宿等级</p>
        <el-dropdown>
          <span class="el-dropdown-link">
            不限
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <div class="shangxia">
              <!--               <el-checkbox
                v-model="checked1"
                v-for="(item,index) in ['1星','2星','3星','4星']"
                :key="index"
                :label="item"
              ></el-checkbox>-->

              <el-checkbox label="1星"></el-checkbox>
              <el-checkbox label="2星"></el-checkbox>
              <el-checkbox label="3星"></el-checkbox>
              <el-checkbox label="4星"></el-checkbox>
             
            </div>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>

      <!-- 类型 -->
      <el-col class="leixing">
        <p class="demonstration">住宿类型</p>
        <el-dropdown>
          <span class="el-dropdown-link">
            不限
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <div class="shangxia">
              <el-checkbox label="经济型"></el-checkbox>
              <el-checkbox label="舒适型"></el-checkbox>
              <el-checkbox label="高档型"></el-checkbox>
              <el-checkbox label="豪华型"></el-checkbox>
              <el-checkbox label="度假村"></el-checkbox>
              <el-checkbox label="公寓式酒店"></el-checkbox>
            </div>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>
      <!-- 酒店设施 -->
      <el-col class="leixing">
        <p class="demonstration">酒店设施</p>
        <el-dropdown>
          <span class="el-dropdown-link">
            不限
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <div class="shangxia">
              <el-checkbox label="wifi"></el-checkbox>
              <el-checkbox label="热水壶"></el-checkbox>
              <el-checkbox label="吹风机"></el-checkbox>
              <el-checkbox label="洗衣服务"></el-checkbox>
              <el-checkbox label="电梯"></el-checkbox>
            </div>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>

      <!-- 酒店品牌 -->
      <el-col class="leixing">
        <p class="demonstration">酒店品牌</p>
        <el-dropdown>
          <span class="el-dropdown-link">
            不限
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <div class="shangxia">
              <el-checkbox label="七天连锁"></el-checkbox>
              <el-checkbox label="汉庭"></el-checkbox>
              <el-checkbox label="如家"></el-checkbox>
              <el-checkbox label="海友"></el-checkbox>
              <el-checkbox label="99"></el-checkbox>
              <el-checkbox label="速八"></el-checkbox>
            </div>
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
      valueed: null,


    };
  }
};
</script>

<style scoped lang='less'>
.xuanze {
  display: flex;
  height: 108px;
  border-top: 1px solid #eee;
}
.el-col {
  padding-top: 10px;
}
.fudu {
  float: right;
  padding-right: 5px;
}
.shangxia {
  width: 140px;
  height: 160px;
  border: 1px solid #eee;

  padding-top: 5px;
}
</style>