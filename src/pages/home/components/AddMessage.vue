<template>
    <div class="message barrages-drop">
        <div style="width:100%;overflow:hidden">
            <vue-baberrage
                style="width:100%;height:100%"
                :isShow= "barrageIsShow"
                :barrageList = "messList"
                :maxWordCount="30"
                :loop = "barrageLoop"
                >
                </vue-baberrage>
        </div>
        <div class="mess-body container ">
                <h1 class="mess-title blog-animation"><i class="el-icon-chat-line-square"></i>Speak freely!</h1>
                <new-comment class="blog-animation comment" @submit="submit"></new-comment>
        </div>
        <span @click="next('#next')" class="screen-next iconfont">
            &#xe623;
        </span>
    </div>
</template>
<script>
import NewComment from './NewComment'
import { vueBaberrage,MESSAGE_TYPE  } from 'vue-baberrage'
export default {
   name:'AddMessage',
   components:{
       NewComment,
       vueBaberrage
   },
   props:{
       list:Array
   },
   data(){
        return {
            messSub:false,
            barrageIsShow: true,
            currentId : 0,
            barrageLoop: true,
            messList:[],
            style:['green','red','blue','green','yellow'],
            FormData:{
                message:'',
                article_id:0,
            }
        }
   },
   methods:{
       next(target){
        let toElement = document.querySelector(target);
            toElement.scrollIntoView({
            behavior: 'smooth',
            block: 'start',
            inline: 'nearest'
            })
        },
       submit(comment){
           this.FormData.message=comment.content
            this.FormData.ip= comment.ip
            this.FormData.address= comment.address
           if(comment.name){
                 this.FormData.tourist=comment.name
           }
           if(comment.qq){
                this.FormData.qq=comment.qq
           }
            // 使用 vue-router 路由到指定页面，该方式称之为编程式导航
            let that=this
            this.$post('/apis/message/'+comment.type,this.FormData)
            .then(function(res){
                that.$emit("submit");
                that.$message({
                    showClose: true,
                    message: res.message,
                    type: 'success'
                });
            })
            .catch(function(error){

            })
          } 
   },
    watch:{
        list(){
            let length=this.list.length
            if(length<=20){
                let i=0
                if(this.list.length>10){
                    i=Math.floor((this.list.length-1)/10)*10
                }
                console.log(i)
                for(i;i<length;i++){
                    this.messList.push({
                        id: this.list[i].id,
                        avatar:this.list[i].user?this.list[i].user.avatar_url:'http://api.btstu.cn/sjtx/api.php?lx=c1&format=images',
                        msg: this.list[i].message,
                        time: Math.ceil(Math.random()*5+4),
                        barrageStyle:this.style[ Math.ceil(Math.random()*4)]
                    });  
                }
            }
            // this.list.forEach(element => {
            //     this.messList.push({
            //         id: element.id,
            //         avatar:element.user?element.user.avatar_url:'http://api.btstu.cn/sjtx/api.php?lx=c1&format=images',
            //         msg: element.message,
            //         time: Math.ceil(Math.random()*5+4),
            //         barrageStyle:this.style[ Math.ceil(Math.random()*4)]
            //     });  
            // });

        }
    }
}
</script>
<style lang="stylus">
@import '~@/assets/style/home.styl';
    .message
        height 100vh
        min-height 500px
        position relative
        // padding  50px 10px
        box-sizing border-box
        // background: url(https://p.pstatp.com/origin/1375d00015657e11e0124)
        background: url(https://p.pstatp.com/origin/ffc700028f5ab952b5da)
        background-repeat:no-repeat;
        background-position:center;
        background-size: cover;
        .mess-body
            position: absolute;
            top: 10%;
            left: 50%;
            transform: translateX(-50%);
            &:hover
                .mess-title
                    color: #5adcce;
            .mess-title
                margin 30px
                font-size 60px
                color #fff
            .blog-animation
                margin 10px
            .comment
                background rgba(255,255,255,.2)
                transition all .5s
                &:hover
                    background rgba(255,255,255,.8)
    @media(max-width: 850px)
        .message
           .mess-title
                font-size 35px!important
       
</style>
<style lang="stylus" scoped>
.barrages-drop >>>
    .baberrage-item
        padding 0
        padding-right 20px
        .normal
            background-color:transparent
.barrages-drop >>>
    .blue {
        border-radius: 100px;
        background: rgba(230, 255, 117, 0.7);
        color: #fff;
    }

    .green {
        border-radius: 100px;
        background: rgba(117, 255, 204, 0.7);
        color: #fff;
    }
    .red {
        border-radius: 100px;
        background: rgba(230, 143, 187, 0.7);
        color: #fff;
    }
    .yellow {
        border-radius: 100px;
        background: rgba(223, 200, 149, 0.7);
        color: #fff;
    }
</style>