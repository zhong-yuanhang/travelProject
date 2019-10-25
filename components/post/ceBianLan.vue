<template>
  <div class="">
    <div class="aside_nav fl clearfix">
      <div class="sidebar clearfix" v-for="(item,index) in form" :key="index">
        <div class="sidebar_index clearfix">
          <div class="left fl">{{item.type}}</div>
          <div class="right fr">></div>
          <div class="clearfix">
            <ul class="sidebar-two">
              <li class="sidebar-info" v-for="(list,index) in item.children" :key="index">
                <span class="index1">{{index + 1}}</span>
                <a href="#" class="index2" @click="tijiao(list.city)">{{list.city}}</a>
                <a href="#" class="index3" @click="tijiao(list.city)">{{list.desc}}</a>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="sidebar-tuiJian">
      <div class="tuiJian-title">
        <h3>推荐城市</h3>
      </div>
      <img src="http://157.122.54.189:9093/images/pic_sea.jpeg" />
    </div>
    </div>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: [],
      city:"",
    };
  },
  methods:{
    tijiao(city){
      this.city = city;
      
      this.$emit("handleCity",city)
      // this.$store.commit("post/setCity",city)
    }
  },
  mounted() {
    // console.log(this.form);

    //请求列表数据
    this.$axios({
      url: "/posts/cities"
    }).then(res => {
      const { data } = res.data;
      console.log(data);

      this.form = data;
    });
  }
};
</script>
        

<style scoped lang="less">
.sidebar {
  .sidebar_index {
    display: inline-block;
    width: 220px;
    font-size: 14px;
    padding: 0 20px;
    height: 42px;
    line-height: 42px;
    border-right: 1px solid #ddd;
    border-bottom: 1px solid #ddd;
  }
}
.sidebar_index:first-child{
  border-top: 1px solid #ddd;
}
.sidebar_index:hover{
  color: #ffa500;
  border-right: none;
}
.sidebar-two {
      position: absolute;
      top: 0px;
      left: 260px;
      width: 350px;
      z-index: 999;
      background: #fff;
      .sidebar-info{
        display:none;
        height: 47px;
        line-height: 47px;
        border-left: 1px solid #ddd;
        border-right: 1px solid #ddd;
        .index1 {
          font-size: 25px;
          font-style: italic;
          color: #ffa500;
          padding: 20px;
          :hover{
            text-decoration: underline;
          }
        }
        .index2 {
          font-size: 16px;
          color: #ffa500;
          :hover{
            text-decoration: underline;
          }
        }
        .index3 {
          font-size: 16px;
          color: #ddd;
          :hover{
            text-decoration: underline;
          }
        }
      }
      .index2:hover{
        text-decoration: underline;
      }
      .index3:hover{
        text-decoration: underline;
      }
      .sidebar-info:first-child{
        border-top: 1px solid #ddd;
      }
      .sidebar-info:last-child{
        border-bottom: 1px solid #ddd;
      }
      .sidebar-info:nth-child(-n+4){
        border-left:none; 
      }
      }
      .sidebar_index:hover .sidebar-info{
        display: block;
      }
    
.aside_nav {
  width: 620px;
  border-left: 1px solid #ddd;
  position:relative;
}

.sidebar-tuiJian {
  width: 260px;
  margin-top: 20px;
  .tuiJian-title {
    padding-bottom: 10px;
    border-bottom: 1px solid #ddd;
    margin-bottom: 10px;
    font-size: 14px;
    h3 {
      font-weight: normal;
    }
  }
  img {
    width: 100%;
  }
}
.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
.fl {
  float: left;
}
.fr {
  float: right;
}
</style>