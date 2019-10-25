<template>
  <div class="list">
    <!-- 头部标题 -->
    <div class="list-head">
      <h3 class="list-head-title">推荐攻略</h3>
      <nuxt-link to="/post/articles"><el-button type="primary" class="el-icon-edit fr">写游记</el-button></nuxt-link>
      
    </div>
    <div class="list-body" 
    v-for="(item,index) in this.data.data" 
    :key="index">
      <nuxt-link :to="`/post/detail?id=${item.id}`">
      <!-- 三张图以上的样式 -->
      <div class="listinfo" v-if="item.images.length >= 3">
        <h3 class="listinfo-title">
          <a href="#">{{item.title}}</a>
        </h3>
        <div class="info-list">
          <a href="#">{{item.summary}}</a>
        </div>
        <div class="img-list clearfix">
          <img v-for="(list,index) in item.images" :key="index" :src="list" v-if="index < 3" />
        </div>
        <div class="list-bottom clearfix">
          <div class="list-bottom-left fl">
            <i class="el-icon-location-outline">{{item.cityName}}</i>
            <span>by</span>
            <div class="yongHu">
              <img :src="$axios.defaults.baseURL+item.account.defaultAvatar" />
              {{item.account.nickname}}
            </div>
            <i class="el-icon-view">{{item.watch}}</i>
          </div>
          <div class="list-bottom-right fr">55赞</div>
        </div>
      </div>
      <!-- 单图的样式 -->
      <div class="list-one clearfix" v-if="item.images.length > 0 && item.images.length < 3">
        <img class="fl" :src="item.images[0]" />
        <div class="listinfo listinfo-one fr">
          <h3 class="listinfo-title listone-title">
            <a href="#">{{item.title}}</a>
          </h3>
          <div class="info-list">{{item.summary}}</div>
          <div class="list-bottom clearfix">
            <div class="list-bottom-left fl">
              <i class="el-icon-location-outline">{{item.cityName}}</i>
              <span>by</span>
              <div class="yongHu">
                <img :src="$axios.defaults.baseURL+item.account.defaultAvatar" />
                {{item.account.nickname}}
              </div>
              <i class="el-icon-view">{{item.watch}}</i>
            </div>
            <div class="list-bottom-right fr">55赞</div>
          </div>
        </div>
      </div>
      </nuxt-link>
    </div>
    <!-- 分页组件 -->
    <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="pageIndex"
        :page-sizes="[5, 10, 15, 20]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="data.total"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pageIndex: 1,
      pageSize: 5,
    };
  },
  props: {
    data: {
      type: Object,
      // 默认是空数组，如果用户不传，采取默认值
      default: {}
    }
  },
  methods: {
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
      this.pageSize = val;
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      this.pageIndex = val;
    }
  }
};
</script>

<style scoped lang="less">
.list-body {
  border-bottom: 1px solid #ddd;
}

.list {
  .list-head {
    width: 700px;
    height: 55px;
    justify-content: space-between;
    border-bottom: 1px solid #ddd;
    .list-head-title {
      display: inline-block;
      border-bottom: 2px solid #ffa500;
      padding: 15px 0 16px;
      font-size: 16px;
      color: #ffa711;
      font-weight: normal;
    }
    .el-button {
      margin-top: 7px;
    }
  }
}
.img-list {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
  img {
    display: block;
    width: 220px;
    height: 150px;
    object-fit: cover;
  }
  img:nth-child(2) {
    margin: 0 10px;
  }
}

.listinfo {
  .listinfo-title {
    display: inline-block;
    height: 50px;
    line-height: 50px;
    font-weight: normal;
  }
  .info-list {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    color: #777;
    font-size: 14px;
    margin-bottom: 15px;
  }
}

.list-bottom {
  margin: 20px 0;
  .list-bottom-left {
    font-size: 12px;
    color: #777;
    margin-top: 5px;
    .yongHu {
      float: left;
      color: #ffa500;
      img {
        width: 10px;
        height: 10px;
        border: 50%;
      }
    }
    i {
      margin: 2px;
    }
  }
  .list-bottom-right {
    color: #ffa711;
  }
}

.list-one {
  border-bottom: 1px solid #ddd;
  padding: 5px 0;
  img {
    display: block;
    width: 220px;
    height: 150px;
    object-fit: cover;
    margin: 12px 0;
  }
}
.listinfo-one {
  width: 480px;
  .listone-title {
    font-size: 18px;
    text-overflow: -o-ellipsis-lastline;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 1;
    -webkit-box-orient: vertical;
  }
}


</style>