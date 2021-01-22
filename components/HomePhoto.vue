<template>
  <v-row>
    <v-col cols="12">
      <v-row>
        <v-card
          height="90vh"
          width="100vw"
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
      <v-row align="center" justify="center">
        <v-col cols="auto" md="6">
          <v-card
            color="transparent"
            class="thisText white--text palatinoFont"
            elevation="0"
          >
            <v-card-title>
              "Across the globe, one thing is universally true of the people of Samajilo: We care deeply about what we do and the impact we have with our clients and communities. It is personal to all of us."
            </v-card-title>
            <v-card-text>
              <div class="palatinoFont white--text">
                Prince Shrestha
              </div>
            </v-card-text>
            <v-card-actions>
              meet our leaders
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>

<script>
import { gsap } from 'gsap/dist/gsap'
import ScrollTrigger from 'gsap/dist/ScrollTrigger'
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
  },
  methods: {
    startAnimation () {
      const thisText = '.thisText'
      gsap.registerPlugin(ScrollTrigger)
      gsap.to(thisText, {
        scrollTrigger: {
          trigger: thisText,
          toggleActions: 'play restart none none'
        },
        duration: 2,
        opacity: 1,
        y: -(screen.availHeight / 1.75)
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
</style>
