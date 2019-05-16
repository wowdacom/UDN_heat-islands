<template>
  <div id="app">
    <section id="titlechart">
      <div id="description">
        <h1 class="badge gsap">Simple Tweening</h1>
        <h2>Two examples of basic animation.</h2>
        <ol>
          <li>When no duration is defined for the scene, the tween will simply start playing when the scroll reaches the trigger position.</li>
          <li>If the scene has a duration the progress of the tween will directly correspond to the scroll position.</li>
        </ol>
        <p>
          This example uses the shorthand version of <a href="../../docs/animation.GSAP.html#Scene.setTween">Scene.setTween()</a> to add <a href="http://greensock.com/docs/#/HTML5/GSAP/TweenMax/to/" target="_blank">TweenMax.to()</a> animations.<br>
          To see how to build more advanced tweens check out the <a href="../advanced/advanced_tweening.html">Advanced Tweening Example</a><a>.
        </a></p><a>
        </a><a href="#" class="viewsource">view source</a>
      </div>
    </section>
    <section class="demo">
      <div class="spacer s2"></div>
      <div id="trigger1" class="spacer s0"></div>
      <div id="animate1" class="box2 skin">
        <p>You wouldn't like me, when I'm angry!</p>
        <a href="#" class="viewsource">view source</a>
      </div>
      <div class="spacer s2"></div>
    </section>
    <section class="demo">
      <div class="spacer s1"></div>
      <div id="trigger2" class="spacer s1"></div>
      <div class="spacer s0"></div>
      <div id="animate2" class="box1 black">
        <p>Smurf me!</p>
        <a href="#" class="viewsource">view source</a>
      </div>
      <div class="spacer s2"></div>
    </section>
    <div class="spacer s_viewport"></div>
     <!-- <ScrollVideo 
        video-name="v0"
        video-time="time"
        video-scroll="scroll"
        video-set-height="set-height"
        video-src="http://nmdap.udn.com.tw/upf/newmedia/2019_data/heat_island/wind_2.mp4"
        video-src-mp4="http://nmdap.udn.com.tw/upf/newmedia/2019_data/heat_island/wind_2.mp4" >
    </ScrollVideo> -->
    <!-- <div ref="set-height" id="set-height"></div>
    <p id="time"></p>
    <video @click="handleVideoChange" ref="v0" id="v0" tabindex="0" autobuffer="autobuffer" preload="preload">
      <source type="video/webm; codecs=&quot;vp8, vorbis&quot;" src="../public/test1.mp4"></source>
      <source type="video/mp4; codecs=&quot;avc1.42E01E, mp4a.40.2&quot;" src="../public/test1.mp4"></source>
      <p>Sorry, your browser does not support the &lt;video&gt; element.</p>
    </video> -->
    
    <button @click="handleVideoChange">切換影片</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ScrollVideo from './components/ScrollVideo.vue'
import test1 from  "../public/test1.mp4"
import test2 from  "../public/test2.mp4"
import test3 from  "../public/test3.mp4"
import test4 from  "../public/test4.mp4"
import { setTimeout } from 'timers';
import ScrollMagic from 'scrollmagic'

export default {
  name: 'app',
  data () {
    return {
      currentVideoSource: require("../public/test1.mp4"),
      currentVideo: 0,
      videoList: [test1, test2, test3, test4],
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
    cureentVideo () {
      let vm = this
      this.currentVideoSource = this.videoList[vm.currentVideo]
      return currentVideoSource
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  #set-height  {
    display: block;
  }
  #v0 {
    position: fixed ;
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
  
}
</style>