<template>
  <div  ref="enter" class="ScrollVideo" data-sticky-container>
    <div class="video-height" :id="videoSetHeight">
      <div class="section-wrapper">
        <div class="section">
          <h1>Hello1</h1>
        </div>
        <div class="section">
          <h1>Hello2</h1>
        </div>
        <div class="section">
          <h1>Hello3</h1>
        </div>
        <div class="section">
          <h1>Hello4</h1>
        </div>
      </div>
    </div>
    <div class="video-time" :id="videoTime"></div>
    <div class="video-scroll" :id="videoScroll"></div>
    <div id="either-gif-or-video">
      <video  class="video-player sticky" data-margin-top="0" data-sticky-for="1023" data-sticky-class="is-sticky" :id="videoName" :src="video1" autobuffer autoplay loop muted playsinline></video>
      <source type="video/webm; codecs=&quot;vp8, vorbis&quot;" :src="video1" webkit-playsinline="true"></source>
      <source type="video/ogg; codecs=&quot;theora, vorbis&quot;" :src="video1"></source>
      <source type="video/mp4; codecs=&quot;avc1.42E01E, mp4a.40.2&quot;" :src="video1"></source>
      <p>Sorry, your browser does not support the &lt;video&gt; element.</p>
      <img src="image.gif">
    </div>
  </div>
</template>

<script>
import { clearInterval } from 'timers';
import Sticky from 'sticky-js'


export default {
  name: 'ScrollVideo',
  data () {
      return {
          vid: null,
          time: null,
          scroll: null,
          windowheight: null,
          scrollpos: window.pageYOffset/50,
          targetscrollpos: null,
          accel: 0,
          accelamount: 0.01,
          bounceamount: 0,
          intervalMark: 0,
          videoPosition: 0,
          video1: require("../../public/wind_3.mp4")
      }
  },
  props: {
    videoName: String,
    videoTime: String,
    videoScroll: String,
    videoSetHeight: String,
    videoSource: String,
    videoSourceMp4: String
  },
  mounted () {
      // console.log(this.videoName)
      // console.log(this.videoTime)
      // console.log(this.videoScroll)
      // console.log(this.videoSetHeight)

      let vm = this
      this.vid = document.getElementById(this.videoName);
      this.time = document.getElementById(this.videoTime);
      this.scroll = document.getElementById(this.videoScroll);
      this.windowheight = window.innerHeight-20;
      this.targetscrollpos = this.scrollpos
      this.vid.pause();
      this.vid.currentTime = 25
      window.addEventListener('scroll', this.handleScroll);

      // console.log('vid:', this.vid)
      // console.log('time:', this.time)
      // console.log('scroll:', this.scroll)
      // console.log('windowheight:', this.windowheight)
      // console.log('scollpos:', this.scrollpos)
      // console.log('targetsscrollpos:', this.targetscrollpos)
      // console.log('accel:', this.accel)
      // console.log('accelamount:', this.accelamount)
      // console.log('bounceamount:', this.bounceamount)

      this.videoPosition = this.getCoords(this.$refs['enter']).top
      
      this.intervalMark = setInterval(function(){  
        
            //Accelerate towards the target:
            vm.accel += (vm.targetscrollpos - vm.scrollpos)*vm.accelamount;
            
            //clamp the acceleration so that it doesnt go too fast
            if (vm.accel > 1) vm.accel = 1;
            if (vm.accel < -1) vm.accel = -1;
        
            //move the video scroll position according to the acceleration and how much bouncing you selected:
            vm.scrollpos = (vm.scrollpos + vm.accel) * (vm.bounceamount) + (vm.targetscrollpos * (1-vm.bounceamount));
        
            //move the blue dot to a position across the side of the screen
            //that indicates where the current video scroll pos is.
            // vm.time.style.top = 10+(window.pageYOffset/4000*this.windowheight)  
        
            //update video playback
            vm.vid.currentTime = vm.scrollpos;
            console.log(vm.scrollpos)
            vm.vid.pause();
            
        }, 40);
  },
  methods: {
      handleScroll () {
        let currentH = window.pageYOffset

        var sticky = new Sticky('.sticky');

        // and when parent change height..
        

        console.log(this.videoPosition)

        if ( this.videoPosition < currentH && currentH < this.videoPosition + 4000) {
          this.targetscrollpos = (window.pageYOffset - this.videoPosition)/500;
          this.scroll.style.top = 10+(window.pageYOffset/1200*this.windowheight)
          sticky.update();
        }
        sticky.destroy();
      },
      getCoords(elem) { // crossbrowser version
          var box = elem.getBoundingClientRect();

          var body = document.body;
          var docEl = document.documentElement;

          var scrollTop = window.pageYOffset || docEl.scrollTop || body.scrollTop;
          var scrollLeft = window.pageXOffset || docEl.scrollLeft || body.scrollLeft;

          var clientTop = docEl.clientTop || body.clientTop || 0;
          var clientLeft = docEl.clientLeft || body.clientLeft || 0;

          var top  = box.top +  scrollTop - clientTop;
          var left = box.left + scrollLeft - clientLeft;

          return { top: Math.round(top), left: Math.round(left) };
      }
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll);
    clearInterval(this.intervalMark)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.ScrollVideo {
    position: relative;
    .video-height {
        display: block;
        height: 4000px;
    }
    .video-player {
        position: absolute;
        height: 100vh;
        z-index: -100;
    }
    p font-family helvetica {
        font-size: 24px;
    }
    .video-time {
        position: absolute;
        display: block;
        top: 10px;
        right: 10px;
        z-index: 2;
        width: 10px;
        height: 10px;
        border-radius: 20px;
        background-color: rgba(0,0,255,0.5);
    }
    .video-scroll {
        position: absolute;
        display: block;
        top: 10px;
        right: 10px;
        z-index: 2;
        width: 10px;
        height: 10px;
        border-radius: 20px;
        background-color: rgba(255,0,0,0.5);
        z-index: -100;
    }
    .section-wrapper {
      height: 400vh;
      width: 100%;
      color: white;
      z-index: 100;
      .section {
        height: 1000px;
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }
    
}
</style>