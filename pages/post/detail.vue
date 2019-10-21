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
            <h1>出发地机场_三亚凤凰机场</h1>
            <span class="art_time">
                <span>攻略: 2019-05-22 </span>
                <span>阅读: 1193</span>
            </span>
            <div class="content">
                <p>我始终还记得那年夏天你为了在我路过的城市见我冒着大雨开车几百公里，只为在车站短短的停留……我也记得在街头只因我看了一眼那各式的冰糖葫芦，你穿越熙攘的人群排队为我拿回最后一个糖葫芦欣喜的样子，不是爱吃甜食的我那晚一口气吃掉了那个糖葫芦，而你看着我憋得满嘴和通红的脸只是宠溺的笑笑……我还记得因为我随口一说自己都没在意的东西而你却把它买回来了，就在有次离别的车站，当我不告而别你知道后发疯的电话、视频和在机场着急的身影，手里还提着我自己也不知道什么时候说过的东西时我就知道你就是那个惊艳了时光也温柔了我曾经岁月的人。</p>
                <img src="../../static/th03.jpg" alt="" height="400px" width="100%">
            </div>

            <div class="icongroup">
                <div>
                    <span class="iconfont">&#xe507;</span>
                    <p>评论(100)</p>
                </div>
                <div>
                    <span class="iconfont">&#xe502;</span>
                    <p>收藏</p>
                </div>
                <div>
                    <span class="iconfont">&#xe601;</span>
                    <p>分享</p>
                </div>
                <div>
                    <span class="iconfont">&#xe604;</span>
                    <p>点赞(54)</p>
                </div>        
            </div>

            
            
            <div class="my-reply">
                <span class="title">评价</span>
                <div class="reply-info" >
                    <!--<div tabindex="0" contenteditable="true" id="replyInput" spellcheck="false" placeholder="输入评论..." class="reply-input"  style="padding: 8px; border: 2px solid blue;"></div>-->
                    <el-input
                    type="textarea"
                    :rows="2"
                    placeholder="说点什么把...."
                    v-model="textarea"
                    >
                    </el-input>
                </div>
                <div class="reply-btn-box" style="" data-v-8d099d26="">
                    <button type="button" class="el-button reply-btn el-button--primary el-button--medium">
                        <!---->
                        <!---->
                        <span>发表评论</span>
                    </button>
                </div>
                <el-upload
                    action="https://jsonplaceholder.typicode.com/posts/"
                    list-type="picture-card"
                    :on-preview="handlePictureCardPreview"
                    :on-remove="handleRemove">
                    <i class="el-icon-plus"></i>
                </el-upload>
                <el-dialog :visible.sync="dialogVisible" size="tiny">
                    <img width="100%" :src="dialogImageUrl" alt="">
                </el-dialog>
            </div>

            
    <div class="author-title reply-father">
        <el-avatar class="header-img" :size="40"></el-avatar>
        <div class="author-info">
            <span class="author-name"></span>
            <span class="author-time"></span>
        </div>
        <div class="icon-btn">
            <span>
                <i class="iconfont el-icon-s-comment"></i></span>
            <i class="iconfont el-icon-caret-top"></i>
        </div>
        <div class="talk-box">
            <p>
                <span class="reply"></span>
            </p>
        </div>
        <div class="reply-box">
            <div  class="author-title">
                <el-avatar class="header-img" :size="40"></el-avatar>
                <div class="author-info">
                    <span class="author-name"></span>
                    <span class="author-time"></span>
                </div>
                <!--点击出现回复部分-->
                <div class="icon-btn">
                    <span >
                        <i class="iconfont el-icon-s-comment"></i></span>
                    <i class="iconfont el-icon-caret-top"></i>
                </div>
                <!--游客回复部分-->
                <div class="talk-box">
                    <p>
                        <span>回复 :</span>
                        <span class="reply"></span>
                    </p>
                </div>
                <div class="reply-box">

                </div>
            </div>
        </div>
        <div  class="my-reply my-comment-reply">
            <el-avatar class="header-img" :size="40" ></el-avatar>
            <div class="reply-info">
                <div tabindex="0" contenteditable="true" spellcheck="false" placeholder="输入评论..."  class="reply-input reply-comment-input"></div>
            </div>
            <div class=" reply-btn-box">
                <el-button class="reply-btn" size="medium"  type="primary">发表评论</el-button>
            </div>
        </div>
    </div>

        </el-main>
        <!--右侧边栏的攻略部分-->
        <el-aside width="250px">
            <p class="title">相关攻略</p>
            <div class="vipgonglue">
                <div class="left">
                    <img src="../../static/th03.jpg">
                </div>
                <div class="right">
                    <p>桂林踩点</p>
                    <p class="vipgonglue_time">
                        <span>2019-05-22 11:45</span>
                        <span>阅读: 1193</span>
                    </p>
                </div>
            </div>
            <div class="vipgonglue">
                <div class="left">
                    <img src="../../static/th03.jpg">
                </div>
                <div class="right">
                    <p>桂林踩点</p>
                    <p class="vipgonglue_time">
                        <span>2019-05-22 11:45</span>
                        <span>阅读: 1193</span>
                    </p>
                </div>
            </div>
            <div class="vipgonglue">
                <div class="left">
                    <img src="../../static/th03.jpg">
                </div>
                <div class="right">
                    <p>桂林踩点</p>
                    <p class="vipgonglue_time">
                        <span>2019-05-22 11:45</span>
                        <span>阅读: 1193</span>
                    </p>
                </div>
            </div>
            <div class="vipgonglue">
                <div class="left">
                    <img src="../../static/th03.jpg">
                </div>
                <div class="right">
                    <p>桂林踩点</p>
                    <p class="vipgonglue_time">
                        <span>2019-05-22 11:45</span>
                        <span>阅读: 1193</span>
                    </p>
                </div>
            </div>
            <div class="vipgonglue">
                <div class="left">
                    <img src="../../static/th03.jpg">
                </div>
                <div class="right">
                    <p>桂林踩点</p>
                    <p class="vipgonglue_time">
                        <span>2019-05-22 11:45</span>
                        <span>阅读: 1193</span>
                    </p>
                </div>
            </div>
        </el-aside>
     </el-container>
  </div>
</template>

<script>
export default {
    data() {
      return {
        dialogImageUrl: '',
        dialogVisible: false,
        textarea: ''
      };
    },
    methods: {
      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePictureCardPreview(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
      }
    }

}
</script>

<style scoped lang="less">

*{
    
}
.container{
    width:1000px;
    margin:0 auto;
    .el-main{
        overflow: visible;
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
            padding: 20px 0;
            border-bottom: 1px solid #ddd;        
    }
    .art_time{
            font-size: 0.8rem;
            line-height: 3.24rem;
            text-align: right;
            color: #999;
            padding: 20px;
            margin-left: 460px;
            span{
                margin-left: 20px;
            }
    }
    .content{
        p{
            margin-bottom:25px;
        }
        img{
            // padding-bottom:80px;
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
            padding-bottom: 14px;
            /deep/ .el-textarea__inner {
                resize:none
            }
        }
        .reply-btn-box{
            position:absolute;
            top:122px;
            right:0px;
        }
    }
    

    //右侧边栏
    .title{
        font-size: 20px;
        border-bottom: 1px #ccc solid;
        padding:29px 0 16px 0;

    }
    .vipgonglue{
        display: block;
        padding:15px 0;
        border-bottom: 1px #ccc solid;
        display: flex;
        .left{
            padding-right:8px;

            img{
                width: 85px;
                height: 62px;
            }
        }
        .right{
            p:nth-child(1){
                padding-bottom:25px;
            }
            p:last-child{
                font-size:12px;
            }
        }
    }
    
}



.el-main {
    background-color: #E9EEF3;
    color: #333;
    line-height: 25px;
}

.el-aside {
    background-color: #D3DCE6;
    color: #333;
    line-height: 20px;

}



body>.el-container {
    margin-bottom: 40px;
}

</style>

