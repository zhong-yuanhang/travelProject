<template>
  <div class="container">
      <el-container>
        <!--左边的详情部分-->
        <el-main>
            <div class="nav">
                <span>
                    <span class="traval-gl">旅游攻略</span>
                    <span class="xian">＞</span>
                </span>
                <span class="gl-detail">
                    <span>攻略详情</span>
                </span>
            </div>
            <div v-for="(item,index) in detail"
            :key="index"> 
                <h1>{{item.title}}</h1>
                <span class="art_time">
                    <span>攻略: {{item.created_at | Upper}} </span>
                    <span>阅读: {{item.watch}}</span>
                </span>
                <div class="content">
                    <p v-html="item.content"></p>
                </div>

                <div class="icongroup">
                <div @click="handleFocus">
                    <span class="iconfont" >&#xe600;</span>
                    <p>评论({{item.comments.length}})</p>
                </div>
                <div @click="handleStar">
                    <span class="iconfont">&#xe602;</span>
                    <p>收藏</p>
                </div>
                <div>
                    <span class="iconfont">&#xe601;</span>
                    <p>分享</p>
                </div>
                <!--点赞功能-->
                <div @click="handleLike" :class="{like_active:detail.like}">
                    <span class="iconfont">&#xe604;</span>
                    <p>点赞({{item.like}})</p>
                </div>        
            </div>
            </div>
            
            

            
            
            <div class="my-reply">
                <span class="title">评价</span>
                <div class="reply-info">
                    <!--<div tabindex="0" contenteditable="true" id="replyInput" spellcheck="false" placeholder="输入评论..." class="reply-input"  style="padding: 8px; border: 2px solid blue;"></div>-->
                    <el-input
                    type="textarea"
                    :rows="2"
                    placeholder="说点什么把...."
                    v-model="textarea"
                    @focus="handleFocus"
                    ref="textarea"
                    >
                    </el-input>
                </div>
                <!--发送按钮和上传框-->
                <div class="publish" v-show="isFocus">
                    <div class="reply-btn-box" >
                    <button type="button" class="el-button reply-btn el-button--primary el-button--medium">
                        <!---->
                        <!---->
                        <span>发表评论</span>
                    </button>
                    </div>
                    <div class="upload">
                        <el-upload
                            action="https://jsonplaceholder.typicode.com/posts/"
                            list-type="picture-card"
                            :on-preview="handlePictureCardPreview"
                            :on-remove="handleRemove"
                            >
                            <i class="el-icon-plus"></i>
                        </el-upload>
                        <el-dialog :visible.sync="dialogVisible" size="tiny">
                            <img width="50%" :src="dialogImageUrl" alt="">
                        </el-dialog>
                    </div>
                </div>
                
            </div>

            <!--评论部分的内容-->
            <div class="author-title reply-father"
            v-for="(item,index) in dataList"
            :key="index+1"
            >   
                <!--用户的头像-->
                <el-avatar class="header-img" :size="40">
                    <img 
                    :src="$axios.defaults.baseURL + item.account.defaultAvatar"
                    v-if="item.account.defaultAvatar">
                    <img src="../../static/th03.jpg" v-else>
                </el-avatar>
                <!--用户的信息-->
                <div class="author-info">
                    <span class="author-name" v-if="item.account.nickname">{{item.account.nickname}}</span>
                    <span class="author-name" v-else>小明</span>
                    <span class="author-time">{{item.account.created_a | Upper}}</span>
                </div>
                <div class="icon-btn1">
                    <span @click="handleNew">
                        <i class="iconfont">&#xe656;</i>{{item.level}}
                    </span>
                        <i class="iconfont">&#xe61e;</i>15
                </div>
                <div class="talk-box">
                    <p>
                        <span class="reply">{{item.content}}</span>
                    </p>
                </div>
                
                <!--回复内容-->
                <CommentFloor v-if="item.parent" :data="item.parent"/>

                <!--消息的回复输入框-->
                <div  class="my-reply my-comment-reply">
                    <el-avatar class="header-img" :size="40" >
                        <img :src="$axios.defaults.baseURL + item.account.defaultAvatar" v-if="item.account.defaultAvatar">
                        <img src="../../static/th03.jpg" v-else>
                    </el-avatar>
                    <div class="reply-info" >
                            <div tabindex="0" contenteditable="true" spellcheck="false" placeholder="输入评论..."    class="reply-input reply-comment-input"></div>
                    </div>
                    <div class="reply-btn-box">
                        <el-button class="reply-btn" size="medium"  type="primary">发表评论</el-button>
                    </div>
                </div>
            </div>

 
 
  <div class="block">
    <!--<span class="demonstration">完整功能</span>-->
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="pageIndex"
      :page-sizes="[2, 4, 6, 8]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="comments.length">
    </el-pagination>
  </div>

        </el-main>
        <!--右侧边栏的攻略部分-->
        <el-aside width="300px">
            <p class="title">相关攻略</p>
            <div 
            v-for="(item,index) in list"
            :key="index+2"
            >
                <nuxt-link :to="`/post/detail?id=${item.id}`" >
                <!--<nuxt-link :to="`/post/`">-->
                    <div @click="handleRefresh" class="vipgonglue">
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
                    </div>
                </nuxt-link>
            </div>
        </el-aside>
     </el-container>

  </div>
</template>

<script>
import moment from "moment";
import CommentFloor from "@/components/post/CommentFloor"

export default {
    //组件的名字，单纯的针对当前的组件可以通过该名字自己调用自己
    name:"name",
    data() {
      return {
        dialogImageUrl: '',
        dialogVisible: false,
        textarea: '',
        //从flights总列表数据中切割出来数组列表
        dataList: [],
        //当前的页数
        pageIndex:1,
        //当前的条数
        pageSize:2,
        //总条数
        total:'',
        //攻略文章的详情
        detail:{},
        //相关攻略列表
        list:[],
        //输入框是否获取焦点
        isFocus:false,
        //评论列表
        comments:[]

      }
    },
    //注册组件
   components:{
        CommentFloor
    },
    
    methods: {

      //分页条数切换时候触发，val是当前的条数  
      handleSizeChange(val) {
          //切换条数
          this.pageSize = val;
          //重新回到第一页
          this.dataList = this.comments.slice(0,this.pageSize)
      },


      //页数切换时候触发,val是当前的页数
      handleCurrentChange(val) {
        //修改当前的页数
        this.pageIndex = val;
        //修改回复列表
        //
        this.dataList = this.comments.slice(
            (this.pageIndex - 1) * this.pageSize,
            this.pageIndex * this.pageSize
        )
      }, 
      

      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePictureCardPreview(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
      },
      
      //点赞
      handleLike(){
          //通过文章id点赞
          this.$axios({
              url:"/posts/like?id=" + this.detail[0].id,
              //添加头信息
              headers:{
                  Authorization: `Bearer ${this.$store.state.user.userInfo.token}`
              }
          }).then(res => {
              const {message} = res.data;
              if(message === '用户已经点赞'){
                    //修改点赞的按钮的状态
                    this.detail.like = false;
                    
              }
          })
      },
      //点赞
      handleStar(){
          //通过文章id收藏
          this.$axios({
              url:"/posts/star?id=" + this.detail[0].id,
              //添加头信息
              headers:{
                  Authorization: `Bearer ${this.$store.state.user.userInfo.token}`
              }
          }).then(res => {
              console.log(res)
          })   
      },
       //获取焦点的时候触发 
       handleFocus(){
           this.isFocus = true;
           this.$refs.textarea.focus();
           
       },
       //点击消息
       handleNew(){
           this.isFocus = ture;
       },
       //重新加载页面(有问题)
       handleRefresh(){
            this.$axios({
                url:"/posts/?id="+id 
            }).then(res => {
                const {data} = res.data;    
                //保存到详情
                this.detail = data;
                this.detail.created_at = moment(this.detail.created_at).format(`YYYY-MM-DD h:mm:ss`);
            })
       }
                   
},
// 声明一个本地的过滤器
    filters: {
           //value代表的是过滤的值
    　　　　Upper: function (value) {
           return moment(value).format(`YYYY-MM-DD h:mm:ss`);
        }   
        
　　  },
    
    mounted(){  
        //请求攻略文章的详情
        const {id} = this.$nuxt.$route.query;
        this.$axios({
            url:"/posts/?id="+id 
        }).then(res => {
            const {data} = res.data;    
            //保存到详情
            this.detail = data;
            console.log('1231231231',this.detail);
            this.detail.created_at = moment(this.detail.created_at).format(`YYYY-MM-DD h:mm:ss`);
           
        }),


        //获取相关攻略的列表(推荐文章)
            this.$axios({
                url:"/posts/recommend"
            }).then(res => {
                const {data} = res.data;
                this.list = data;
                
        })
        //请求文章评论
        // const {id} = this.$route.params;
           this.$axios({
               url:"/posts/comments/",
           }).then(res => {
                const {data} = res.data;
                this.comments = data;
                // console.log(this.comments)

                //第一页的数据
                this.dataList = this.comments.slice(0,this.pageSize)
                
                // this.dataList = this.comment.length;
           }) 
           

    }

}
</script>

<style scoped lang="less">

.container{
    width:1000px;
    margin:0 auto;
    .el-main{
        overflow: visible;
        line-height: 25px;
    }
    .nav{
        .traval-gl{
            font-weight: 700;
            text-decoration: none;
            
            color: #303133;
        }
        .traval-gl:hover{
            color:#409eff;
            transition: color .5s;
            cursor:pointer;
        }
        .gl-detail{
            font-weight: 400;
            color: #606266;
        }
        .xian{
            margin: 0 9px;
            font-weight: 700;
            color: #c0c4cc;
        }
    }
    h1{
        font-size: 31px;
        padding: 20px 0;
        border-bottom: 1px solid #ddd;   
        line-height: 40px;     
    }
    .art_time{
            font-size: 16px;
            line-height: 3.24rem;
            text-align: right;
            color: #999;
            padding: 20px;
            display:flex;
            justify-content: flex-end;;
            span{
                margin-left: 20px;
            }

    }
    .content{
    /deep/p{
                margin-bottom:25px; 
                img{
                    max-width: 700px!important;
                }
                span{
                    img{
                        max-width: 700px!important;
                    }  
                }      
            }    
    }
    .icongroup{
        display:flex;
        justify-content: center;
        text-align: center;
        padding: 50px 0 30px;
        .iconfont{
            font-family: "iconfont" !important;
            // display: block;
            margin: 0 20px;
            font-size: 32px;
            color: orange;
            font-style: normal;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            cursor:pointer;
        }
        .like_active{
            color:red;
        }
    }
    .my-reply{
        position:relative;
        // background-color: #fafbfc;
        .title{
            font-weight: 400;
            font-size: 18px;
            margin-bottom: 20px;
            border-bottom:none;
        }
        .reply-info{
            padding-top: 28px;
            // padding-bottom: 14px;
            /deep/ .el-textarea__inner {
                resize:none;
                border: 2px solid #DCDFE6;
            }
            /deep/ .el-textarea__inner:focus {
                outline: 0;
                border-color: #409EFF;
            }

        }
        .publish{
            margin-bottom:10px;
            width:100px;
            .reply-btn-box{
                position:absolute;
                top:125px;
                right:0px;
            }

            .upload{
                /deep/.el-upload--picture-card{
                    margin-top: 10px;
                    background-color: #fbfdff;
                    border: 1px dashed #c0ccda;
                    border-radius: 6px;
                    box-sizing: border-box;
                    width: 52px;
                    height: 52px;
                    line-height: 54px;
                    vertical-align: top;
                }
            }
        }
        

    }

    .author-title{
        position: relative;
        padding-bottom: 10px;
        border-bottom: 1px solid #ccc;
        margin-top: 10px;
        .header-img{
            display: inline-block;
            vertical-align: top;
        }
        .author-info{
            display: inline-block;
            margin-left: 5px;
            .author-name{
                color: #000;
                font-size: 18px;
                font-weight: bold;
                display: block;
            }
            .author-time{
                font-size: 14px;
                display:block;
                margin-top:-5px;
            }

        }
        .icon-btn1{
            position: absolute;
            top:0px;
            right:20px;
            span{
                cursor: pointer;
            }
        }
        .icon-btn{
            position: absolute;
            top:5px;
            right:10px;
            span{
                cursor: pointer;
            }

        }
        .talk-box{
            padding-left: 50px;
            p{  
                margin-top:5px;
                margin-bottom: 10px;
            }
                
        }
        .reply-box{
            margin-left: 50px;
            background-color:#efefef;
            .author-title{
                padding:10px;
                border-bottom: 1px solid #ccc; 
            }
            .author-title:last-child{
                border-bottom:none;
            }
        }
        .my-reply{
            margin-left: 50px;
            padding-top:10px;
            position: relative;
            height: 100px;
            background-color: #fafbfc;
            .header-img{
                margin-left: 10px;
            }
            .reply-info {
                display: inline-block;
                margin-left: 5px;
                width: 76%;
                position: absolute;
                top: -16px;
                left: 58px;
                
                .reply-input{
                    min-height: 20px;
                    line-height: 22px;
                    padding: 10px 10px;
                    color: #ccc;
                    background-color: #fff;
                    border-radius: 5px;
                    &:empty:before{
                        content: attr(placeholder);
                    }
                    &:focus:before{
                        content: none;
                    }
                    &:focus{
                        padding: 8px 8px;
                        border: 2px solid #409eff;
                        box-shadow: none;
                        outline: none;
                    }
                }
     
            }
            .el-button{
                    margin-top:15px;
                    float:right;
                    margin-right:25px;
                }
        }
    }
    .block{
        margin-top:10px;
        padding:0 10px;
    }   
    
}





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



body>.el-container {
    margin-bottom: 40px;
}
              

</style>

