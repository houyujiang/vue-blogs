<template>
    <div class="messa">
        <add-message  @submit="getMess"  :list="list"></add-message>
        <div class="mess-bg" >
            <add-link></add-link>
            <message-list :list="list"  @submit="getMess"></message-list>
            <p class="next" ><span v-loading="loading" element-loading-text="拼命加载中"
    element-loading-spinner="el-icon-loading"
    element-loading-background="#f8f8f8"  @click="next"><i class="next-icon" :class="current_page==last_page?'el-icon-arrow-up':'el-icon-arrow-down'"></i>  {{current_page==last_page?'没有更多了！快去留言吧！^o^':'点击查看更多'}}</span></p>
        </div>
    </div>
</template>
<script>
import AddMessage from '../components/AddMessage'
import AddLink from '../components/AddLink'
import MessageList from '../components/MessageList'

export default {
    name:'Message',
    components:{
        AddLink,
        AddMessage,
        MessageList,
    },
    data(){
        return {
            list:[],
            current_page:1,
            last_page:1,
            loading:false
        }
    },
    methods:{
        getMessList(){
            var that=this;
            this.loading=true
            that.$get('/apis/message/list?id=0&'+'page='+that.current_page)
            .then(function(res){
                that.list=that.list.concat(res.data.data)
                that.last_page=res.data.last_page
                that.current_page=res.data.current_page
                that.loading=false
            })
            .catch(function(error){
                that.loading=false
            })
        },
         getMess(){
                var that=this;
                that.$get('/apis/message/list?id='+that.$route.params.id+'&page=1')
                .then(function(res){
                    that.list=res.data.data
                    that.last_page=res.data.last_page
                    that.current_page=res.data.current_page
                })
                .catch(function(error){
                })
          },
          next(){
              if(this.current_page<this.last_page){
                  this.current_page++
                  this.getMessList()
              } 
          }
    },  
    created() {
       this.getMessList()
    },
}
</script>
<style lang="stylus" scoped>
.messa
    background-color #f8f8f8
    padding-bottom:15px
    .next
        text-align center
        color:var(--main-5)
        transition all .3s
        &:hover
            color:var(--main-6)
        span 
            cursor pointer
            .next-icon
                 animation: next .6s linear infinite alternate;
@keyframes next {
    0%{
        transform translateY(3px)
    }
    100%{
        transform translateY(0px)
    }
}    
</style>
