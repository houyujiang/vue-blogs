<template>
  <div class="route">
    <!-- <el-carousel height="400px">
                <el-carousel-item v-for="item in 4" :key="item">
                    <h3 class="small">{{ item }}</h3>
                </el-carousel-item>
    </el-carousel>-->
    <div class="container">
      <h1 class="mess-title blog-animation" style="margin-top:20px">
        <i class="el-icon-goods"></i>个人项目
      </h1>
      <div style="height:260px">
        <el-carousel
          v-if="carousel.length>0"
          class="blog-animation"
          :interval="4000"
          :type="card"
          height="200px"
          style="padding:10px 0"
        >
          <el-carousel-item
            v-for="item in carousel"
            :key="item.id"
            :style="{'background-color': setColor(),'background-image':'url('+item.imgUrl+')'}"
          >
            <a :href="item.link" target="_blank">
              <div class="medium">
                <h4 class="route-title">{{ item.name }}</h4>
                <p class="route-content">{{item.info}}</p>
              </div>
            </a>
            <el-avatar :size="40" class="car-img" shape="square" fit="fit" :src="item.imgUrl">
              <img src="https://p.pstatp.com/origin/1379300008dada52a7875" />
            </el-avatar>
          </el-carousel-item>
        </el-carousel>
      </div>

      <h1 class="mess-title blog-animation">
        <i class="el-icon-reading"></i>成长路线
      </h1>
      <route-list :list="list"></route-list>
    </div>
  </div>
</template>

<script>
import RouteList from "./../components/RouteList";
export default {
  name: "GrowthRoute",
  components: {
    RouteList,
  },
  data() {
    return {
      list: [],
      card: document.body.clientWidth > 885 ? "card" : "",
      carousel: [],
    };
  },
  methods: {
    setColor() {
      let r = parseInt(Math.random() * 256);
      let g = parseInt(Math.random() * 256);
      let b = parseInt(Math.random() * 256);
      return `rgba(${r},${g},${b},0.3)`;
    },
    change(x) {
      console.log(this.list[x].content);
      this.title = this.list[x].category;
      this.content = this.list[x].content;
    },
    getRoute() {
      let that = this;
      that
        .$get("/apis/route/list")
        .then(function (res) {
          that.list = res.data;
        })
        .catch(function (error) {});
    },
    getCarousel() {
      let that = this;
      that
        .$get("/apis/link/list?type=1")
        .then(function (response) {
          console.log(response);
          that.carousel = response.data;
        })
        .catch(function (error) {
          // console.log(error.data);
        });
    },
  },
  created() {
    this.getRoute();
    this.getCarousel();
  },
};
</script>
<style lang="stylus" scoped>
@import '~@/assets/style/home.styl';

.route {
  // background:$color url('../../../assets/routebg.jpg')
  // background-repeat:no-repeat;
  // background-attachment:fixed;
  // background-position:center;
  // background-size: cover;
  background-color: #f8f8f8;

  // z-index:-4
  &:hover {
    .mess-title {
      color: #5adcce;
    }
  }

  >>>.el-carousel__mask {
    display: block !important;
  }

  .medium {
    text-align: center;
    margin-top: 50px;
    padding: 0 10%;

    // background:rgba(255,255,255,.5)
    .route-title {
      font-size: 30px;
      routeHover();
    }
  }

  .mess-title {
    margin: 0;
    font-size: 25px;
    color: #ccc;
    ellipsis();
  }

  .el-carousel__item h3 {
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
  }

  .el-carousel__item {
    backdrop-filter: blur(20px);
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    // filter: blur(20px);
  }

  .el-avatar {
    position: absolute;
    top: 5px;
    left: 50%;
    transform: translateX(-50%);
    background: transparent;
  }
}
</style>