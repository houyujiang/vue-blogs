<template>
    <!-- <div class="container-fluid footer" v-show="route!='/blog'">
            <p class="link a-tag">
                <router-link to="/">主页</router-link>|
                <router-link to="/blog">博客</router-link>|
                <router-link to="/message">留言</router-link>|
                <router-link to="/route">成长</router-link>|
                <router-link to="/link">友链</router-link>
            </p>
            <p>© 2020 - {{year}} 云墨白 All Rights Reserved.</p>
            <a class="a-flex" target="_blank" href="https://www.upyun.com/?utm_source=lianmeng&utm_medium=referral"><span>本网站由</span><img class="ypy" src="~@/assets/logo8.png"><span>提供CDN加速/云存储服务</span></a>
		 	<a class="a-flex" target="_blank" href="http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=34030002020734" ><img class="logo" src="~@/assets/备案图标.png" /><span>皖公网安备 34030002020734号</span></a>
            <a target="_blank" href="http://www.beian.miit.gov.cn/">皖ICP备2020014908号-1</a>
    </div> -->
    <footer class="footer" v-show="route!='/blog'">
        <div class="container">
            <div class="foot-row service">
                <p class="title">Baymax•记录美好学习时光，分享学习点点滴滴</p>
                    <ul class="link">
                        <li><router-link to="/link">友链</router-link></li>

                        <li><router-link to="/route">成长</router-link></li>

                        <li><router-link to="/message">留言</router-link></li>

                        <li><router-link to="/blog">博客</router-link></li>

                        <li><router-link to="/">主页</router-link></li>
                    </ul>
            </div>
            <div class="foot-row provide">
                <span><a class="a-flex" target="_blank" href="https://www.upyun.com/?utm_source=lianmeng&utm_medium=referral"><span>本网站由</span><img class="ypy" src="~@/assets/logo8.png"><span>提供CDN加速/云存储服务</span></a></span>
                <div class="search-wrap">
                    <form
                        method="get"
                        action="//google.com.hk/search"
                        target="_blank"
                        autocomplete="off"
                    >
                        <input type="hidden" name="oe" value="UTF-8" />
                        <input type="hidden" name="hl" value="zh-CN" />
                        <input type="hidden" name="domains" value="www.yunmobai.cn" />
                        <input type="hidden" name="ie" value="UTF-8" />
                        <input type="hidden" name="sitesearch" value="www.yunmobai.cn" />
                        <input
                            class="search-ipt"
                            type="text"
                            placeholder="find something…"
                            name="q"
                            spellcheck="false"
                            maxlength="40"
                        />
                        <button type="submit" class="icon">
                        <i class="icon-search  el-icon-search"></i>
                        </button>
                    </form>
                </div>
            </div>
            <div class="foot-row publicity">
                <span><a target="_blank" href="http://www.beian.miit.gov.cn/">皖ICP备2020014908号-1</a></span>
                <span><a class="a-flex" target="_blank" href="http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=34030002020734" >皖公网安备 34030002020734号</a></span>
            </div>
            <hr/>
            <div class="foot-row bottom">
                <p class="copyright">© 2020 - {{year}} <a href="http://www.yunmobai.cn/">云墨白</a> All Rights Reserved.<a target="_blank" href="/apis/sitemap">网站地图</a></p>
                <div class="share">
                        <a target="_blank" href="http://wpa.qq.com/msgrd?v=3&uin=2401694354&site=qq&menu=yes" class="iconfont qq" title="使用QQ账号登录" @click="partyLogin('qq')">&#xe651;</a>
                        <a target="_blank" href="https://gitee.com/baymaxsjj" class="iconfont gitee" title="使用Gitee登录" @click="partyLogin('gitee')">&#xe686;</a>
                        <a target="_blank" href="https://github.com/baymaxsjj" class="iconfont github" title="使用GitHub登录" @click="partyLogin('github')">&#xe691;</a>
                </div>
            </div>
        </div>
    </footer>
    
</template>
<script>
export default {
    name:'IndexFooter',
    props:{
      route:String
    },
    data(){
        return{
            year:2020,
        }
    },
   created(){
       let date=new Date();
       this.year=date.getFullYear()
   }
}
</script>
<style lang="stylus" scoped>
    .footer
        padding: 10px 30px;
        font-size 12px
        color #a7a7a7
        // background:rgba(248, 249, 250, 0.9)
        background:#fff
        font-weight:bolder
        letter-spacing: 2px;
        padding:10px
        line-height 26px
        a
            color #a7a7a7
            font-size 12px
            transition all .3s
            &:hover
                text-decoration underline 
        .container
            padding 0 10px
            box-sizing: border-box;
            .foot-row
                display: flex;
                justify-content space-between
                align-items: center;
                flex-wrap wrap 
            .service
                font-size 16px
                .link
                    li
                        
                        float right
                        margin 0 20px
                        a
                            font-size 14px
            .provide
                .a-flex
                    display: flex;
                    justify-content:stretch;
                    align-items: center;
                    .ypy
                        height 22px
                .search-wrap 
                    width: 300px;
                    height 22px
                    position: relative;
                    padding 2px 0
                    .search-ipt 
                        height 20px
                        position absolute 
                        right 0
                        top 0
                        width: 240px;
                        color: var(--main-6);
                        background: none;
                        border: none;
                        border-bottom: 2px solid var(--main-1);
                        font-family: Roboto, serif;
                        font-size: 1rem;
                        line-height: 1.75;
                        transition all .4s
                        &:focus
                            width 100%
                    .icon 
                        outline:none;
                        background-color: transparent;
                        border: none;
                        padding 7px
                        line-height 0
                        position: absolute;
                        right: 0;
                        color: var(--main-4);
                        cursor: pointer;
           
            hr
                background-color #f0f0f0
            .bottom
                .share
                    .iconfont
                        display inline-block
                        height 30px
                        width 30px
                        line-height 28px
                        font-size:16px
                        margin:5px
                        cursor pointer
                        color #a7a7a7
                        border-radius 50%
                        text-align center
                        transition all .5s
                        box-sizing border-box
                        &:hover  
                            text-decoration none 
                    .qq
                        // color rgb(27,193,250)
                        // border 1px solid rgb(27,193,250)
                        &:hover
                            color #fff
                            background-color rgb(27,193,250)
                    .gitee
                        // color  #fe7300
                        // border 1px solid  #fe7300
                        &:hover
                            color #fff
                            background-color #fe7300
                    .github
                        // color  #0a0203
                        // border 1px solid  #0a0203
                        &:hover
                            color #fff
                            background-color #0a0203 

                    

            
     @media(max-width: 700px)
        .footer
            padding 10px
            font-size 12px
            letter-spacing: 2px;
            line-height 24px
            .container
                padding 0!important
                .foot-row
                    justify-content center!important
                .service
                    .title
                        font-size 14px
                    .link
                        li
                            margin 0 5px!important
                .provide
                    .search-wrap
                        padding 1px 0!important
                        .search-ipt 
                            right 50%!important
                            transform translateX(50%)
                .publicity
                    span 
                        margin 0 5px
                .bottom
                    .copyright
                        letter-spacing: 1px;
                
</style>