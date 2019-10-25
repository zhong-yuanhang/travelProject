<template>
    <!--回复内容-->
    <div class="reply-box" v-if="data">
        <div class="author-title">
            <el-avatar class="header-img" :size="40">
                <!--<img :src="$axios.defaults.baseURL + data.account.defaultAvatar" v-if="data.account.defaultAvatar">
                <img src="../../static/th02.jpg" v-else>-->
                <img src="../../static/th03.jpg" v-if="`../../static/th03.jpg`">
                <img :src="$axios.defaults.baseURL + data.account.defaultAvatar" v-else>
                
            </el-avatar>
            <div class="author-info">
                <span class="author-name">{{data.account.nickname}}</span>
                <span class="author-time">{{data.created_at | Upper}}</span>
            </div>
            <!--点击出现回复部分-->
            <div class="icon-btn">
                <span>
                    <i class="iconfont">&#xe656;</i>2
                </span>
                <i class="iconfont">&#xe61e;</i>15
            </div>
            <!--游客回复部分-->
            <div class="talk-box">
                <p>
                    <span>回复 <strong>{{data.account.nickname}}</strong>:{{data.content}}</span>
                    <span class="reply"></span>
                </p>
            </div>
            <div class="reply-box">

            </div>
        </div>

        <!--自己再次在这个位置调用自己-->
        <comment :data="data.parent"/>
    </div>
</template>

<script>
import moment from "moment";
export default {
    //组件的名字，单纯的针当前组件的命名，当前的组件可以通过该名字自己调用自己
    name:"comment",
    props:["data"],
    // 声明一个本地的过滤器
    filters: {
           //value代表的是过滤的值
    　　　　Upper: function (value) {
           return moment(value).format(`YYYY-MM-DD h:mm:ss`);
　　　　    console.log(value)
        }   
        
　　  },
    
}
</script>

<style scoped lang="less">
.art_time {
    font-size: 16px;
    line-height: 3.24rem;
    text-align: right;
    color: #999;
    padding: 20px;
    display: flex;
    justify-content: flex-end;
    ;
    span {
        margin-left: 20px;
    }
}

.content {
    /deep/p {
        margin-bottom: 25px;
        img {
            max-width: 700px!important;
        }
        span {
            img {
                max-width: 700px!important;
            }
        }
    }
}

.icongroup {
    display: flex;
    justify-content: center;
    text-align: center;
    padding: 50px 0 30px;
    .iconfont {
        font-family: "iconfont" !important; // display: block;
        margin: 0 20px;
        font-size: 32px;
        color: orange;
        font-style: normal;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        cursor: pointer;
    }
}

.my-reply {
    position: relative; // background-color: #fafbfc;
    .title {
        font-weight: 400;
        font-size: 18px;
        margin-bottom: 20px;
        border-bottom: none;
    }
    .reply-info {
        padding-top: 28px; // padding-bottom: 14px;
        /deep/ .el-textarea__inner {
            resize: none;
            border: 2px solid #DCDFE6;
        }
        /deep/ .el-textarea__inner:focus {
            outline: 0;
            border-color: #409EFF;
        }
    }
    .publish {
        margin-bottom: 10px;
        width: 100px;
        .reply-btn-box {
            position: absolute;
            top: 125px;
            right: 0px;
        }

        .upload {
            /deep/.el-upload--picture-card {
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

.author-title {
    position: relative;
    padding-bottom: 10px;
    border-bottom: 1px solid #ccc;
    margin-top: 10px;
    .header-img {
        display: inline-block;
        vertical-align: top;
    }
    .author-info {
        display: inline-block;
        margin-left: 5px;
        .author-name {
            color: #000;
            font-size: 18px;
            font-weight: bold;
            display: block;
        }
        .author-time {
            font-size: 14px;
            display: block;
            margin-top: -5px;
        }
    }
    .icon-btn1 {
        position: absolute;
        top: 0px;
        right: 20px;
        span {
            cursor: pointer;
        }
    }
    .icon-btn {
        position: absolute;
        top: 5px;
        right: 10px;
        span {
            cursor: pointer;
        }
    }
    .talk-box {
        padding-left: 50px;
        p {
            margin-top: 5px;
            margin-bottom: 10px;
        }
    }
    .reply-box {
        margin-left: 50px;
        background-color: #efefef;
        .author-title {
            padding: 10px;
            border-bottom: 1px solid #ccc;
        }
        .author-title:last-child {
            border-bottom: none;
        }
    }
    .my-reply {
        margin-left: 50px;
        padding-top: 10px;
        position: relative;
        height: 100px;
        background-color: #fafbfc;
        .header-img {
            margin-left: 10px;
        }
        .reply-info {
            display: inline-block;
            margin-left: 5px;
            width: 76%;
            position: absolute;
            top: -16px;
            left: 58px;

            .reply-input {
                min-height: 20px;
                line-height: 22px;
                padding: 10px 10px;
                color: #ccc;
                background-color: #fff;
                border-radius: 5px;
                &:empty:before {
                    content: attr(placeholder);
                }
                &:focus:before {
                    content: none;
                }
                &:focus {
                    padding: 8px 8px;
                    border: 2px solid #409eff;
                    box-shadow: none;
                    outline: none;
                }
            }
        }
        .el-button {
            margin-top: 15px;
            float: right;
            margin-right: 25px;
        }
    }
}

.block {
    margin-top: 10px;
    padding: 0 10px;
}



body>.el-container {
    margin-bottom: 40px;
}
</style>