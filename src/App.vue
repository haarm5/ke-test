<script>
import { ref } from 'vue'
import { reactive } from 'vue'

export default {
  data() {
    return {
      maxVol: 1
    }
  },
  computed: {
    // มองเป็น resolver
  },
  mounted() {
    // มองเป็น ngOninit
    const videoElement = this.$refs.videoElement
    const audioElement1 = this.$refs.audioElement1
    const audioElement2 = this.$refs.audioElement2
    videoElement.play()
    audioElement1.play()
    audioElement2.play()

    const volumeSlider = document.getElementById('volumeSlider')
    volumeSlider.addEventListener('input', (e) => {
      const volume = parseFloat(e.target.value)
      this.maxVol = volume
      audioElement1.volume = volume
      audioElement2.volume = volume
    })

    const volumeMusic = document.getElementById('volumeMusic')
    volumeMusic.addEventListener('input', (e) => {
      const volume = parseFloat(e.target.value)
      audioElement1.volume = volume
      // audioElement2.volume = volume
    })
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
      const audioElement1 = this.$refs.audioElement1
      const audioElement2 = this.$refs.audioElement2

      this.selectedTime = videoElement?.currentTime
      audioElement1.currentTime = this.selectedTime
      audioElement2.currentTime = this.selectedTime
      videoElement.pause()
      audioElement1.pause()
      audioElement2.pause()

      videoElement.play()
      audioElement2.play()
      audioElement1.play()
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

  <label style="margin-top: 20px">เพิ่มลดเสียง</label>
  <br />
  <input type="range" id="volumeSlider" min="0" max="1" :step="maxVol / 20" value="1" />

  <br />

  <label style="margin-top: 20px">เพิ่มลดเสียง</label>
  <br />
  <input type="range" id="volumeMusic" min="0" :max="1" :step="0.05" :value="1" />
  <br />
  <button @click="muteMusic" style="margin-top: 20px">เปิด-ปิด เสียงเพลง</button>
  <br />
  <button @click="muteVocals">เปิด-ปิด เสียงร้อง</button>
</template>

<style>
video::-webkit-media-controls-volume-slider {
  display: none !important;
}
video::-webkit-media-controls-mute-button {
  display: none !important;
}
</style>
