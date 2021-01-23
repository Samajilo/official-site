<template>
  <div>
      <v-main v-scroll="documentScrolled">
        <div class="slides-container">
          <div class="slide" id="slide-1">
            <VintageWithText />
          </div>
          <div class="slide" id="slide-2">
            <DiscoverHistoryLink />
          </div>
          <div class="slide" id="slide-3">
            <DiscoverHistoryLink />
          </div>
        </div>
      </v-main>
  </div>
</template>

<script>
import { gsap } from 'gsap/dist/gsap'
import TweenLite from 'gsap'
import ScrollToPlugin from 'gsap/dist/ScrollToPlugin'
// import HomePhoto from '../components/HomePhoto'
import VintageWithText from '../components/VintageWithText'
import DiscoverHistoryLink from '../components/DiscoverHistoryLink'

export default {
  name: 'indexPage',
  components: {
    VintageWithText,
    DiscoverHistoryLink
  },
  data () {
    return {
      slides: [
        'slide-1',
        'slide-2',
        'slide-3'
      ],
      lastLocation: 0,
      currentSlide: '',
      animating: false,
      keycodes: {
        UP: 38,
        DOWN: 40
      },
      pageHeight: 0
    }
  },
  mounted () {
    this.lastLocation = window.pageYOffset
    this.currentSlide = this.slides[0]
    gsap.registerPlugin(TweenLite, ScrollToPlugin)
    this.pageHeight = window.innerHeight
  },
  methods: {
    documentScrolled(e) {
      if (this.lastLocation >  window.pageYOffset) {
        this.lastLocation = window.pageYOffset
        this.previousSlide()
      } else if (this.lastLocation < window.pageYOffset) {
        this.lastLocation = window.pageYOffset
        this.nextSlide()
      }
    },
    previousSlide(){
      let index = this.slides.indexOf(this.currentSlide)
      index -= 1
      this.goToSlide(index)
    },
    nextSlide () {
      let index = this.slides.indexOf(this.currentSlide)
      index += 1
      this.goToSlide(index)
    },
    goToSlide(slide) {
      let thisContainer = '.slides-container'
      if(!this.animating && this.slides.length) {
        this.animating = true;
        this.currentSlide = this.slides[slide];
        gsap.to(window, {duration: 1.5, scrollTo: this.pageHeight * slide, ease: "power2", onComplete: this.onSlideChangeEnd}).eventCallback(this.onSlideChangeEnd);
        console.log(this.pageHeight * slide)
      }
    },
    onSlideChangeEnd() {
      this.animating = false;
    }
  }
}
</script>
