<template>
  <div id="app">
    <transition name="fade" mode="out-in" appear>
    <router-view/>
</transition>
  </div>
  
</template>

<script>
import '@/assets/scss/main.scss'
import $ from 'jquery'
export default {
  name: 'App',
  data () { return { index:0 } },
   components: {
  },
  computed: {
    user() {
      return this.$store.state.user
    },
    
  },
   methods: {
   heartbeat () {
      this.axios.get(process.env.VUE_APP_API + '/users/heartbeat')
        .then(res => {
          // 如果 vuex 是登入中
          if (this.user.id.length > 0) {
            // 但是後端沒登入
            if (!res.data) {
              this.$swal({
                icon: 'error',
                title: '錯誤',
                text: '登入時效已過'
              })
              // 登出
              this.$store.commit('logout')
              // 導回首頁
              if (this.$route.path !== '/') {
                this.$router.push('/')
              }
            }
          }
        })
        .catch(() => {
          this.$swal({
            icon: 'error',
            title: '錯誤',
            text: '發生錯誤'
          })
          // 登出
          this.$store.commit('logout')
          // 導回首頁
          if (this.$route.path !== '/') {
            this.$router.push('/')
          }
        })
    },
    scroller () {
        $(window).scroll(function(){
        if($(window).scrollTop() > 100)
        {
          $(".navbar-nav").addClass("scrollTop")
          $(".nav-link").css("color",'#fff')
        }
         else if(
          $(window).scrollTop() < 40)
          {$(".navbar-nav").removeClass("scrollTop")
          $(".nav-link").css(
            "color","#818181",
            "font-weight","heavy"
          )}
   })
    },
   },
  mounted () {
    this.heartbeat()
    setInterval(() => {
      this.heartbeat()
    }, 5000)
    this.scroller()
    
  }
}
</script>



<style lang="scss">
  // .slide-left-enter-active { animation: slideLeft 0.4s ease-in-out; } 
  // @keyframes slideLeft { from { transform: translate3d(0, 100%,0 );/*橫坐標,縱坐標,z坐標*/ visibility: visible; } 
  // to { transform: translate3d(0, 0, 0); } }
.fade-enter, .fade-leave-to{
  opacity: 0;
}
.fade-enter-active,
.fade-leave-active{
transition: opacity 0.5s;
  
}
</style>