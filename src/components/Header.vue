<template>
    <div>
        <!--头部-->
        <header class="clearfix">
            <a class="icon-back fl" v-if="goBack" @click="goBackUri()">
                <img src="/static/images/icon_back.png" alt="返回">
            </a>
            <router-link to="/" class="logo fl" v-else>
                <img src="/static/images/logo.png" alt="星航">
            </router-link>
            <span class="fs32 c-fff" v-if="headTitle">{{headTitle}}</span>
            <a class="navbox fr" href="javascript:;" @click="isShow=!isShow">
                <img src="/static/images/icon_nav.png" alt="菜单">
            </a>
        </header>
        <transition name="fade">
            <div v-show="isShow" class="nav-modal-box nav-menu">
                <div class="content">
                    <ul>
                        <li v-for="(item,index) in navs" :key="index" :class="item.class" @click="goTo(item.url)">
                            <a href="javascript:;" v-text="item.text"></a>
                        </li>
                    </ul>
                    <img src="/static/images/icon_close.png" alt="关闭" @click="isShow=!isShow">
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isShow: false,
            navs: [
                { url: '/', text: '首页' },
                { url: '/personal', text: '个人通' },
                { url: '/company', text: '企业通' },
                { url: '/enter', text: '走进金服' },
                { url: '/news/groupnews', text: '新闻中心' },
                { url: '/joinus', text: '加入我们' },
                { url: '/contactus', text: '联系我们' },
                { url: '/appdownload', text: 'APP下载', class: 'border-bottom-none' },
            ]
        }
    },
    props: ['headTitle', 'goBack'],
    methods: {
        goTo(url) {
            this.isShow = !this.isShow;
            this.$router.push({ path: url })
        },
        goBackUri() {
            if (this.goBack==='true'){
                this.$router.go(-1)
            }else{
                this.$router.push({ path: this.goBack })
            }
    }
}
}
</script>
<style>
.nav-modal-box {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background: rgba(12, 17, 23, .9);
    z-index: 90;
    text-align: center;
    color: #d3b4a0;
    padding: 0 0.3rem;
    font-size: 0.24rem;
}
</style>