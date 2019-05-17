<template>
  <div id="app">
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
    <p>hello</p>
     <ScrollVideo 
        video-name="v0"
        video-time="time"
        video-scroll="scroll"
        video-set-height="set-height"
        :video-src="video1"
        :video-src-mp4="video1" >
    </ScrollVideo>
    <div class="container">
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
      <p>hello</p>
    </div>
    
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ScrollVideo from './components/ScrollVideo.vue'
import { setTimeout } from 'timers';
import ScrollMagic from 'scrollmagic'

export default {
  name: 'app',
  data () {
    return {
      currentVideo: 0,
      frameNumber: 0,
      playbackConst: 500, 
      setHeight: this.$refs['set-height'],        
      vid: this.$refs['v0'],
      isClick: false
    }
  },
  components: {
    HelloWorld,
    ScrollVideo
  },
  mounted () {
    let vm = this
    
    var controller = new ScrollMagic.Controller();
    console.log(controller)
    var scene = new ScrollMagic.Scene({
									triggerElement: "#trigger1"
								})
								.setTween("#animate1", 0.5, {backgroundColor: "green", scale: 2.5}) // trigger a TweenMax.to tween
								.addIndicators({name: "1 (duration: 0)"}) // add indicators (requires plugin)
                .addTo(controller);
                
    var scene = new ScrollMagic.Scene({triggerElement: "#trigger2", duration: 300})
                // animate color and top border in relation to scroll position
                .setTween("#animate2", {borderTop: "30px solid white", backgroundColor: "blue", scale: 0.7}) // the tween durtion can be omitted and defaults to 1
                .addIndicators({name: "2 (duration: 300)"}) // add indicators (requires plugin)
                .addTo(controller);
    // this.$refs['v0'].addEventListener('loadedmetadata', function() {
    //   vm.$refs['set-height'].style.height = Math.floor(vm.$refs['v0'].duration) * vm.playbackConst + "px";
    // });
    // var line1 = document.querySelector('#line2d_21');
    // var line2 = document.querySelector('#line2d_22');
    // var line3 = document.querySelector('#line2d_23');

    // var path1 = document.querySelector('#line2d_21 > path');
    // var path2 = document.querySelector('#line2d_22 > path');
    // var path3 = document.querySelector('#line2d_23 > path');
    // var length = path.getTotalLength();

    // console.log('hello1:', path1.getTotalLength())
    // console.log('hello2:', path2.getTotalLength())
    // console.log('hello3:', path3.getTotalLength())

    // setTimeout(()=>{
    //   line1.style.strokeDashoffset = 284.5
    // }, 1000)

    // setTimeout(()=>{
    //   line1.style.strokeDashoffset = 0
    // }, 2000)
    // window.requestAnimationFrame(vm.scrollPlay);
  },
  methods: {
    scrollPlay() {  
      // var frameNumber  = window.pageYOffset/ this.playbackConst;
      // this.$refs['v0'].currentTime  = frameNumber;
      // window.requestAnimationFrame(this.scrollPlay);
    },
    handleVideoChange() {
      this.isClick = !this.isClick
      // if(this.currentVideo < this.videoList.length - 1) {
      //   this.currentVideo++
      // } else {
      //   this.currentVideo = 0
      // }
      // this.$refs['v0'].src = this.videoList[this.currentVideo]
    }
  },
  computed: {
  }
}
</script>

<style lang="scss">
body, html {
  margin: 0;
  padding: 0;
}

#app {

  #set-height  {
    display: block;
  }
  #v0 {
    position: absolute ;
    top: 0;
    left: 0;
    width: 100%;
  }
  p {
    font-family: helvetica;
    font-size: 24px;
  }
  svg {
    #line2d_21 {
      stroke-dasharray: 569;
      stroke-dashoffset: 569;
      // animation: dash 3s linear forwards;
    }
    #line2d_22 {
      stroke-dasharray: 569;
      stroke-dashoffset: 569;
      // animation: dash 3s linear forwards;
    }
    #line2d_23 {
      stroke-dasharray: 569;
      stroke-dashoffset: 569;
      // animation: dash 3s linear forwards;
    }
  }

  .unClick {
    animation: dash 3s ease-in-out forwards;
  }

  .isClick {
    animation: dash2 3s ease-in-out forwards;
  }

  @keyframes dash {
  from {
    stroke-dashoffset: 569;
  }
  to {
    stroke-dashoffset: 260;
  }
}

  @keyframes dash2 {
    from {
      stroke-dashoffset: 260;
    }
    to {
      stroke-dashoffset: 0;
    }
  }
  .container {
    margin-top: 100px;
  }
}
</style>