<template>
    <header class="header">
        <!-- 头部的第一行 -->
        <div class="top">
            <div class="container">
                <div class="loginList">
                    <p>尚品汇欢迎您！</p>
                    <p>
                        <span>请</span>
                        <!-- 声明式导航：务必要有to属性 -->
                        <router-link to="/login">登录</router-link>
                        <router-link class="register" to="/register">免费注册</router-link>
                    </p>
                </div>
                <div class="typeList">
                    <a href="###">我的订单</a>
                    <a href="###">我的购物车</a>
                    <a href="###">我的尚品汇</a>
                    <a href="###">尚品汇会员</a>
                    <a href="###">企业采购</a>
                    <a href="###">关注尚品汇</a>
                    <a href="###">合作招商</a>
                    <a href="###">商家后台</a>
                </div>
            </div>
        </div>
        <!--头部第二行 搜索区域-->
        <div class="bottom">
            <h1 class="logoArea">
                <router-link class="logo" to="/home">
                    <img src="./images/logo.png" alt="">
                </router-link>
            </h1>
            <div class="searchArea">
                <form action="###" class="searchForm">
                    <input type="text" id="autocomplete" class="input-error input-xxlarge" v-model="keyWord" />
                    <button class="sui-btn btn-xlarge btn-danger" type="button" @click="goSearch">
                        搜索
                    </button>
                </form>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    name: '',
    data() {
        return {
            keyWord: '',
        }
    },
    methods: {
        // 搜索按钮的回调函数：需要向search路由进行跳转
        goSearch() {
            //路由的跳转,采用的是编程式导航.
            //路由传递参数

            //第一种传递query参数
            // this.$router.push({path:'/search',query:{keyword:this.keyword}});

            //第二种传递params参数 [一定要注意,面试的时候经常问]
            // this.$router.push({name:'search',params:{keyword:this.keyword}})

            //第三种传递query+params
            // this.$router.push({
            //   name: "search",
            //   params: { keyword: this.keyword },
            //   query: { keyword: "ABC" },
            // });

            //验证Vue-Router引入Promise技术,最笨的方法,给push传递第二个、第三个参数【回调函数】
            //下面这种写法：治标不治本！！！！
            // let result = this.$router.push({name: "search",params: { keyword: this.keyword|| undefined}},()=>{},()=>{});

            //问题1:push方法,里面this是谁? vueRouter类的实例
            // this.$router.push({name:'search',params:{keyword:this.keyword}});
            //问题2:push方法里面的this是谁?windows
            // let result = this.$router.push;
            // result({name:'search',params:{keyword:this.keyword}})
            //点击搜索按钮之前,如果路径当中有query参数,需要携带给search

            // 面试题4：路由组件能不能传递props数据？
            // 可以的：三种写法

            // 代表的是如果有query参数也带过去
            if(this.$route.query){
                let location = {name: "search",params: {keyWord: this.keyWord || undefined}};
                location.query = this.$route.query;
                this.$router.push(location)
            }
        }
    }
}
</script>

<style scoped lang="less">
.header {
    &>.top {
        background-color: #eaeaea;
        height: 30px;
        line-height: 30px;

        .container {
            width: 1200px;
            margin: 0 auto;
            overflow: hidden;

            .loginList {
                float: left;

                p {
                    float: left;
                    margin-right: 10px;

                    .register {
                        border-left: 1px solid #b3aeae;
                        padding: 0 5px;
                        margin-left: 5px;
                    }
                }
            }

            .typeList {
                float: right;

                a {
                    padding: 0 10px;

                    &+a {
                        border-left: 1px solid #b3aeae;
                    }
                }

            }

        }
    }

    &>.bottom {
        width: 1200px;
        margin: 0 auto;
        overflow: hidden;

        .logoArea {
            float: left;

            .logo {
                img {
                    width: 175px;
                    margin: 25px 45px;
                }
            }
        }

        .searchArea {
            float: right;
            margin-top: 35px;

            .searchForm {
                overflow: hidden;

                input {
                    box-sizing: border-box;
                    width: 490px;
                    height: 32px;
                    padding: 0px 4px;
                    border: 2px solid #ea4a36;
                    float: left;

                    &:focus {
                        outline: none;
                    }
                }

                button {
                    height: 32px;
                    width: 68px;
                    background-color: #ea4a36;
                    border: none;
                    color: #fff;
                    float: left;
                    cursor: pointer;

                    &:focus {
                        outline: none;
                    }
                }
            }
        }
    }
}
</style>