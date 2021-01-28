<template>
  <v-row class="mt-3">
    <v-col cols="12">
      <v-row>
        <v-card
          height="100vh"
          width="100vw"
          class="thisCardToStart"
        >
          <client-only>
            <v-img
              :lazy-src="randomImagelazy"
              :src="randomImagesrc"
              height="100vh"
              width="100vw"
              max-height="100vh"
              max-width="100vw"
              @load="startAnimation"
            >
              <template v-slot:placeholder>
                <v-row class="fill-height ma-0" align="center" justify="center">
                  <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                  />
                </v-row>
              </template>
            </v-img>
          </client-only>
        </v-card>
      </v-row>
      <v-row align="center" justify="center" style="height:100vh!important">
        <v-col cols="auto" md="5">
          <v-card
            color="transparent"
            class="thisText black--text palatinoFont"
            elevation="0"
          >
            <v-card-title>
              "Across the globe, 
                one thing is universally
                true of the people of
                Samajilo: We care deeply
                about what we do and the
                impact we have
                with our clients
                and communities. It 
                is personal to all of us."
            </v-card-title>
            <v-card-text>
              <div class="palatinoFont black--text">
                Prince Shrestha
              </div>
            </v-card-text>
            <v-card-actions>
              <div id="featureBackground"></div>
              <v-btn
                class="animateBtn"
                id="button"
                small
                rounded
                outlined
              >
                meet our leaders
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
      <div id="featureBackgroundSpark"></div>
    </v-col>
  </v-row>
</template>

<script>
import { gsap } from 'gsap/dist/gsap'
import ScrollTrigger from 'gsap/dist/ScrollTrigger'
import { TimelineMax } from 'gsap'
import { ScrollMagic } from 'scrollscene'
import { ScrollScene } from 'scrollscene'
export default {
  name: 'HomePhoto',
  data () {
    return {
      increaseBorderOnHoverClasses: ['botthonToHover'],
      images: [
        {
          src: '/main_page/one.jpg',
          lazy: '/main_page/one.jpg'
        },
        {
          src: '/main_page/two.jpg',
          lazy: '/main_page/two.jpg'
        },
        {
          src: '/main_page/three.jpg',
          lazy: '/main_page/three.jpg'
        },
        {
          src: '/main_page/four.jpg',
          lazy: '/main_page/four.jpg'
        }
      ],
      randomImagesrc: '',
      randomImagelazy: ''
    }
  },
  mounted () {
    const item = this.images[Math.floor(Math.random() * this.images.length)]
    this.randomImagesrc = item.src
    this.randomImagelazy = item.lazy
    gsap.registerPlugin(ScrollTrigger, TimelineMax, ScrollMagic, ScrollScene)
  },
  methods: {
    startAnimation () {
      const thisText = '.thisText'
      gsap.to(thisText, {
        scrollTrigger: {
          trigger: '.thisCardToStart',
          toggleActions: 'play restart restart none',
          pin: true,
          markers: true,
        },
        duration: 1.5,
        opacity: 1,
      })
    },
    increaseBorderOnHover () {
      this.increaseBorderOnHoverClasses = ['bottonHovered']
    },
    hoverout () {
      this.increaseBorderOnHoverClasses = ['botthonToHover']
    }
  }
}
</script>
<style scoped>
  @import url('http://fonts.cdnfonts.com/css/palatino-linotype');
  .botthonToHover {
    width: 10px!important;
    border: 10px solid red;
  }
  .bottonHovered {
    width: 100px!important;
    border: 10px solid red;
  }
  .spark {
  position: absolute;
  background-color: transparent;
  width: 50px;
  height: 50px;
  border-radius: 50%;
}
</style>
<style lang="scss" scoped>
$bg-color:#536dfe;
.animateBtn {
  color: navy;
  border: none;
  font-size: 1rem;
  background-color: grey;
  z-index: 1;
  padding: 1rem 3rem;
  border-radius: 2rem;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  transition: color 600ms;
  &:before {
    content: "";
    z-index: -1;
    top: 0;
    left: 0;
    position: absolute;
    width: 100%;
    height: 100%;
    background: linear-gradient(-60deg, $bg-color 50%, transparent 50%);
    background-size: 250%;
    transition: background-position 600ms;
    transform: rotate(180deg);
  }
  &:hover, &:focus {    
    color: white;
    &:before {
      background-position: 100% 100%;
      transform: rotate(0deg);
    }
  }
}

</style>
