<template>
  <div class="music">
    <Button title="Play" v-on:button-click='play'></Button>
    <Button title="Pause" v-on:button-click='pause'></Button>
    <Button title="Loop" v-on:button-click='loop'></Button>
    <Button title="Restart" v-on:button-click='restart'></Button>
    <Button title="Next" v-on:button-click='next'></Button>
    <Button title="Previous" v-on:button-click='previous'></Button>
    <Button title="Faster" v-on:button-click='faster'></Button>
    <Button title="Slower" v-on:button-click='slower'></Button>
    Current track: {{ audio.current }}
    Current time: {{ currentTime }} 
    Current Rate: {{ audio.playbackRate }}
  </div>
</template>

<script>
import Button from './Button.vue'

export default {
  name: 'MusicPlayer',
  components: {
      Button,
  },
  data: function() { 
    return { 
      audio: { 
        instance: {},
        current: 1,
        max: 7,
        currentTime: {
          seconds: 0,
          minutes: 0,
        },
        playbackRate: 1,
      }
    }
  },
  computed: {
    currentTime: function() { 
      let onesPlace = this.audio.currentTime.seconds < 10 ? `0${this.audio.currentTime.seconds}` : this.audio.currentTime.seconds;
      return `${this.audio.currentTime.minutes}:${onesPlace}`;
    },
    playbackRate: function() { 
      return this.audio.instance.playbackRate;
    },
  },
  created: function() {
    let song = new Audio(require(`@/assets/sound/Song 1.mp3`));
    song.addEventListener('timeupdate', () => {
      console.log(song.currentTime);
      this.audio.currentTime.seconds = Math.floor(song.currentTime % 60);
      this.audio.currentTime.minutes = Math.floor(song.currentTime / 60);
    });
    song.addEventListener('loadeddata', () => {
      this.audio.instance = song;
    });
  },
  methods: {
    faster() {
      if (this.audio.instance.playbackRate < 1.5) { 
        this.audio.instance.playbackRate += 0.05;
      }
      this.audio.playbackRate = this.audio.instance.playbackRate.toFixed(2);
    },
    loop() { 
      this.audio.instance.loop = this.audio.instance.loop ? false : true;
    },
    next() { 
      this.audio.current = this.audio.current < this.audio.max ? this.audio.current + 1 : 1;
      this.audio.instance.src = require(`@/assets/sound/Song ${this.audio.current}.mp3`);
      this.audio.playbackRate = 1;
      this.play();
    },
    pause() { 
      this.audio.instance.pause();
    },
    play() {
      this.audio.instance.play();
    },
    previous() { 
      this.audio.current = this.audio.current > 1 ? this.audio.current - 1 : 7;
      this.audio.instance.src = require(`@/assets/sound/Song ${this.audio.current}.mp3`);
      this.audio.playbackRate = 1;
      this.play();
    },
    restart() { 
      this.audio.instance.currentTime = 0;
    }, 
    slower() {
      if (this.audio.instance.playbackRate > 0.5) { 
        this.audio.instance.playbackRate -= 0.05;
      }
      this.audio.playbackRate = this.audio.instance.playbackRate.toFixed(2);
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
  .music { 
    width: 30%;
    display: inline-block;
  }
</style>
