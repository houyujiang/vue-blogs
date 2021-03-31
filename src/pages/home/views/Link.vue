<template>
    <div class="link">
        <link-header></link-header>
        <link-friends :friends="friends"></link-friends>
    </div>
</template>
<script>
import LinkHeader from '../components/LinkHeader'
import LinkFriends from '../components/LinkFriends'

export default {
    name:'Link',
    components:{
        LinkHeader,
        LinkFriends,
    },
    data(){
        return {
            friends:[]
        }
    },
    methods:{
       getFriends(){
            let that=this
            that.$get('/apis/link/list?type=0')
            .then(function (response) {
                 that.friends=response.data
            })
            .catch(function (error) {
                // console.log(error.data);
            });
        }
    },
    created(){
        this.getFriends()
    }
}
</script>
<style lang="stylus" scoped>
    .link
        background-color #fff
        .link-bg
            position:fixed
            top:0
            right:0
            bottom:0
            left:0
            margin:auto
            z-index:-1
</style>