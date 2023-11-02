<script>
import { ref } from 'vue'
import { reactive } from 'vue'

export default {
  computed: {
    // มองเป็น resolver
  },
  mounted() {
    // มองเป็น ngOninit
    const videoElement = this.$refs.videoElement
    videoElement.play()
    const audioElement1 = this.$refs.audioElement1
    audioElement1.play()
    const audioElement2 = this.$refs.audioElement2
    audioElement2.play()
  },
  methods: {
    // เขียน methods ในนี้
    muteMusic() {
      const audioElement1 = this.$refs.audioElement1
      if (audioElement1.muted) {
        audioElement1.muted = false
      } else {
        audioElement1.muted = true
      }
    },
    muteVocals() {
      const audioElement2 = this.$refs.audioElement2
      if (audioElement2.muted) {
        audioElement2.muted = false
      } else {
        audioElement2.muted = true
      }
    },
    onSeeked() {
      const videoElement = this.$refs.videoElement
      this.selectedTime = videoElement.currentTime
      const audioElement1 = this.$refs.audioElement1
      const audioElement2 = this.$refs.audioElement2
      audioElement1.currentTime = this.selectedTime
      audioElement2.currentTime = this.selectedTime
    },
    onVideoPlay() {
      const audioElement1 = this.$refs.audioElement1
      const audioElement2 = this.$refs.audioElement2
      audioElement1?.play()
      audioElement2?.play()
    },
    onVideoPause() {
      console.log('pause')
      const audioElement1 = this.$refs.audioElement1
      const audioElement2 = this.$refs.audioElement2
      audioElement1?.pause()
      audioElement2?.pause()
    }
  }
}
</script>

<template>
  <video
    id="myVideo"
    controls
    muted
    width="552"
    height="541"
    ref="videoElement"
    @seeked="onSeeked"
    @play="onVideoPlay"
    @pause="onVideoPause"
  >
    <source src="./assets/video.mp4" type="video/mp4" />
    Your browser does not support the video tag.
  </video>

  <br />
  <audio ref="audioElement1">
    <source src="./assets/music.mp3" type="audio/mp3" />
    Your browser does not support the audio element.
  </audio>
  <audio ref="audioElement2">
    <source src="./assets/vocals.mp3" type="audio/mp3" />
    Your browser does not support the audio element.
  </audio>
  <button @click="muteMusic">ปิดเสียงเพลง</button>
  <br>
  <button @click="muteVocals">ปิดเสียงร้อง</button>
</template>

<style>
.title {
  color: red;
}
</style>
