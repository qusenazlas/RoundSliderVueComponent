<template>
  <div class="round-slider-wrapper">
    <svg :width="this.size" :height="this.size">
      <circle
        :cx="this.size / 2"
        :cy="this.size / 2"
        :r="this.size / 2.5"
        :stroke-width="this.size / 11"
        :stroke="this.stokeColor"
        fill="none"
        class="slider-stroke"
      ></circle>
      <path
        class="active-path"
        :stroke="this.activePathColor"
        fill="none"
        :stroke-width="this.size / 13"
        :d="`M175 35 a 1 1 0 0 1 0 ` + this.slideValue"
      ></path>
      <circle
        :cx="this.size / 2"
        :cy="this.size / 10"
        class="slider-knob"
        :r="this.size / 25"
        :fill="this.knobColor"
        id="knob"
      ></circle>
    </svg>
  </div>
</template>
<script>
export default {
  data() {
    return {
      size: 350,
      lineWidth: 15,
      stokeColor: '#323232',
      knobColor: 'pink',
      activePathColor: 'blue',
      isSlide: false,
      isSlideEnd: false,
      isSlideStart: false,
      slideValue: 0
    }
  },
  methods: {
    onStartSlide() {
      let knob = document.getElementById('knob')
      knob.addEventListener('mousedown', () => {
        this.isSlideStart = true
        this.onSlide()
      })
    },
    onSlide() {
      if (this.isSlideStart) {
        let knob = document.getElementById('knob')
        knob.addEventListener('mousemove', e => {
          this.isSlide = true
          this.activePathCal(e)
        })
      }
    },
    onSlideEnd() {
      let knob = document.getElementById('knob')
      knob.addEventListener('mouseup', this.activePathCal())
    },
    activePathCal(e) {
      if (this.isSlide) {
        //   let mousePositionX = e.offsetX
        let mousePositionY = e.offsetY
        let basePostionX = 175
        //   let basePostionY = 0
        let angle = Math.atan2(mousePositionY, basePostionX)
        console.log(angle)
        this.slideValue = angle.toString()
      }
    }
  },
  mounted() {
    this.onStartSlide()
    this.onSlideEnd()
  }
}
</script>
<style lang="scss" scoped>
@import './RoundSlider.scss';
</style>
