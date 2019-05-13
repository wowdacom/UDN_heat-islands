<template>
  <div id="app">
    <div ref="set-height" id="set-height"></div>
    <p id="time"></p>
    <video @click="handleVideoChange" ref="v0" id="v0" tabindex="0" autobuffer="autobuffer" preload="preload">
      <source type="video/webm; codecs=&quot;vp8, vorbis&quot;" src="../public/test1.mp4"></source>
      <source type="video/mp4; codecs=&quot;avc1.42E01E, mp4a.40.2&quot;" src="../public/test1.mp4"></source>
      <p>Sorry, your browser does not support the &lt;video&gt; element.</p>
    </video>
    <button @click="handleVideoChange">切換影片</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import test1 from  "../public/test1.mp4"
import test2 from  "../public/test2.mp4"
import test3 from  "../public/test3.mp4"
import test4 from  "../public/test4.mp4"

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
      vid: this.$refs['v0']
    }
  },
  components: {
    HelloWorld
  },
  mounted () {
    let vm = this
    console.log()
    this.$refs['v0'].addEventListener('loadedmetadata', function() {
      vm.$refs['set-height'].style.height = Math.floor(vm.$refs['v0'].duration) * vm.playbackConst + "px";
    });

    window.requestAnimationFrame(vm.scrollPlay);
  },
  methods: {
    scrollPlay() {  
      var frameNumber  = window.pageYOffset/ this.playbackConst;
      this.$refs['v0'].currentTime  = frameNumber;
      window.requestAnimationFrame(this.scrollPlay);
    },
    handleVideoChange() {
      if(this.currentVideo < this.videoList.length - 1) {
        this.currentVideo++
      } else {
        this.currentVideo = 0
      }
      this.$refs['v0'].src = this.videoList[this.currentVideo]
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
}
</style>