<template>
    <div>
        <el-aside width="300px" >
            <p class="title">相关攻略</p>
            <div class="vipgonglue" 
            v-for="(item,index) in list" 
            :key="index"
            >
                <nuxt-link :to="`/post/detail?id=${item.id}`">
                    <div class="left">
                        <img :src="item.images[0]" >
                    </div>
                    <div class="right">
                        <p>{{item.title}}</p>
                        <p class="vipgonglue_time">
                            <!--过滤器，直接过滤时间 {{值 | 过滤的方法}}-->
                            <span>{{item.created_at | Upper}}</span>
                            <span>阅读: {{item.watch}}</span>
                        </p>
                    </div>
                </nuxt-link>
            </div>
        </el-aside>
    </div>
</template>

<script>
import moment from "moment";
export default {
    data() {
      return {
        //相关攻略列表
        list:[],

      }
    },
    // 声明一个本地的过滤器
    filters: {
           //value代表的是过滤的值
    　　　　Upper: function (value) {
           return moment(value).format(`YYYY-MM-DD h:mm:ss`);
　　　　    console.log(value)
        }   
        
　　  },
   
    mounted(){

        //获取相关攻略的列表(推荐文章)
            this.$axios({
                url:"/posts/recommend"
            }).then(res => {
                // console.log(res);
                const {data} = res.data;
                this.list = data;
                
                console.log(this.list.created_at);
                console.log(this.list[2]);
            })        

    }
}
</script>

<style scoped lang="less">

.el-aside {

    line-height: 20px;
    //右侧边栏
    .title{
        font-weight: 400;
        font-size: 18px;
        padding-bottom: 10px;
        padding-top:25px;
        border-bottom: 1px solid #ddd;

    }
    .vipgonglue{
        display: block;
        padding:20px 0;
        border-bottom: 1px #ccc solid;
        display: flex;
        cursor: pointer;
        .left{
            padding-right:8px;
            img{
                width: 100px;
                height: 80px;
            }

        }
        .right{
            display:flex;
            flex-direction: column;
            justify-content: space-between;
            p:last-child{
                font-size:12px;
                color: #999;
            }
        }
    }
}
</style>
