<template>
    <div class="slider" ref="slider">
      <div class="slider-group" ref="sliderGroup">
        <slot></slot>
      </div>
    </div>
</template>

<script>
  import BScroll from 'better-scroll'
  import {addClass} from "common/js/dom";

  export default {
    name: "slider",
    props: {
      loop: {
        type: Boolean,
        default: true
      },
      autoPlay: {
        type: Boolean,
        default: true,
      },
      interval: {
        type: Number,
        default: 4000
      }
    },
    mounted() {
      setTimeout(() => {
        this._setSliderWidth()
        this._initSlider()
      }, 20)
    },
    methods: {
      _initSlider() {
        this.slider = new BScroll(this.$refs.slider, {
          scrollX: true,
          scrollY: false,
          momentum: false,
          snap: true,
          snapLoop: this.loop,
          snapThreshold: 0.3,
          snapSpeed: 400
        })
      },
      _setSliderWidth() {
        let children = this.$refs.sliderGroup.children
        let sliderWidth = this.$refs.slider.clientWidth
        let width = 0
        for (let i = 0; i < children.length; i++) {
          let child = children[i]
          addClass(child, 'slider-item')
          child.style.width = sliderWidth + 'px'
          width += sliderWidth
        }
        if(this.loop) {
          width += 2 * sliderWidth
        }
        this.$refs.sliderGroup.style.width = width + 'px'
      }
    },

  }
</script>

<style scoped>

  .slider{
    min-height: 1px
  }
  .slider .slider-group{
    position: relative;
    overflow: hidden;
    white-space: nowrap;
  }
  .slider .slider-item{
    float: left;
    box-sizing: border-box;
    overflow: hidden;
    text-align: center;
  }
  .slider .slider-item a{
    display: block;
    width: 100%;
    overflow: hidden;
    text-decoration: none;
  }
  .slider img{
    isplay: block;
    width: 100%
  }
</style>
