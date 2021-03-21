<template>
<div>
  <Navbar/>
<div class="container  h-100">
  <div class="row ">
   <div class="col-12  brand-intro-outer">
     
  <div class="row">
           <div class="col-12 concept mb-5">
         <p class="concept-title">關於我們</p>
       </div>
  </div>
       <video-background 
    src="../viedos/intro.mp4"

    :sources="[
        {src: '../viedos/intro.mp4', res: 900, autoplay: true}, 
        {src: '../viedos/intro.mp4', res: 638, autoplay: true}
    ]"
    style="max-height: 700px; height: 100vh;"
    overlay="linear-gradient(45deg,#2a4ae430,#fb949e6b)" 
        >
      </video-background>

<div class="brand-intro-container">
    </div>
      <div class="brand-intro-text">
<img src='@/assets/logo.png' class="w-25">
      <span >心電圖結合山的意象<br>
        象徵著人與山林的和諧<br>山林帶給我們一股最原始的悸動
        <br >在山裡找到自己不再迷惘<br>彷彿重獲新生</span>
   </div>
 
  </div>

  </div>
   
  </div>
  </div>
  
</template>

<script>
import Navbar from '../Navbar'
import store from '@/store'

export default {
  name: 'Brand',
  components: {
    Navbar,
    },
  data () {
    return {
       }
  },
  computed: {
    user () {
      return store.state.user
    },
  },
    methods: {
 
    },
   created() {

    }
}
</script>

