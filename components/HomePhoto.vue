<template>
  <v-row class="mt-3">
    <v-col cols="12">
      <v-row>
        <v-card
          height="100vh"
          width="100vw"
          class="thisCardToStart"
          elevation="16"
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
                  <v-progress-circular indeterminate color="grey lighten-5" />
                </v-row>
              </template>
            </v-img>
          </client-only>
        </v-card>
      </v-row>
      <v-row align="center" justify="center" style="height:100vh">
        <v-col cols="auto" md="5">
          <v-card
            color="transparent"
            class="thisText white--text palatinoFont"
            elevation="0"
          >
            <v-card-title>
              "Across the globe,<br />
                one thing is universally true of the people of
                Samajilo: We care deeply about what we do and the impact we have
              with our clients and communities.
              <br/>It is personal to all of us."
            </v-card-title>
            <v-card-text>
              <div
                class="palatinoFont black--text montserrat"
              >
                <router-link to="/prince" class="text-decoration-none">
                  <span>Prince Shrestha</span>
                </router-link>
              </div>
            </v-card-text>
            <v-card-actions
              class="ma-0 mt-5"
            >
              <div class="svg-wrapper"
              >
                <svg height="50" width="180" xmlns="http://www.w3.org/2000/svg">
                  <rect class="shape" height="50" width="180" />
                </svg>
                <v-btn
                  class="text text-h6 noBackgroundOnHover palatinoFont white--text"
                  style="text-transform: none;"
                  @mouseover="buttonHovered"
                  @mouseout="buttonHoverLeave"
                  :class="actionClasses"
                  id="button"
                  small rounded text>
                  meet our leaders
                </v-btn>
              </div>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
      <div id="featureBackgroundSpark"></div>
    </v-col>
  </v-row>
</template>

<script>
import { gsap } from "gsap/dist/gsap";
import ScrollTrigger from "gsap/dist/ScrollTrigger";
import { TimelineMax } from "gsap";
import { ScrollMagic } from "scrollscene";
import { ScrollScene } from "scrollscene";
import "animate.css";
export default {
  name: "HomePhoto",
  data() {
    return {
      images: [
        {
          src: "/main_page/girl.jpg",
          lazy: "/main_page/girl.jpg",
        },
      ],
      randomImagesrc: "",
      randomImagelazy: "",
      actionClasses: [],
      mouseOnPrinceClasses: []
    };
  },
  mounted() {
    const item = this.images[Math.floor(Math.random() * this.images.length)];
    this.randomImagesrc = item.src;
    this.randomImagelazy = item.lazy;
    gsap.registerPlugin(ScrollTrigger);
  },
  methods: {
    buttonHovered(){
      this.actionClasses = ['animate__animated', 'animate__tada']
    },
    buttonHoverLeave(){
      this.actionClasses = []
    },
    startAnimation() {
      const thisText = ".thisText";
      gsap.to(thisText, {
        scrollTrigger: {
          trigger: ".thisCardToStart",
          toggleActions: "play restart restart none",
          pin: true,
          markers: true,
        },
        duration: 1.5,
        opacity: 1,
      });
      gsap.fromTo(
        ".thisCardToStart",
        { opacity: 1 },
        {
          opacity: 0,
          duration: 1,
          scrollTrigger: {
            trigger: ".thisCardToStart",
            start: "bottom center",
            end: "+=300",
            toggleActions: "play restart restart none",
            scrub: 1,
            markers: true,
          },
        }
      );
    },
  },
};
</script>
<style scoped>
@import url("http://fonts.cdnfonts.com/css/palatino-linotype");
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");
.noBackgroundOnHover:hover{
  background-color: transparent !important;
}
.svg-wrapper {
  height: 40px;
	margin: 0;
  position: relative;
  /* top: 50%; */
  transform: translateY(-50%);
  width: 150px;
  -webkit-animation: 0.5s draw linear backwards;
  animation: 0.5s draw linear backwards;
}

.shape {
  fill: transparent;
  stroke-dasharray: 50 540;
  stroke-dashoffset: -294;
  stroke-width: 6px;
  stroke: #19f6e8;
}

.text {
  position: relative;
  top: -48px;
}
@keyframes draw {
  0% {
    stroke-dasharray: 70 540;
    stroke-dashoffset: -294;
    stroke-width: 8px;
  }
  100% {
    stroke-dasharray: 760;
    stroke-dashoffset: 0;
    stroke-width: 4px;
  }
}
.svg-wrapper:hover .shape {
  -webkit-animation: 0.5s draw linear forwards;
  animation: 0.5s draw linear forwards;
}
.montserrat{
  font-family: Montserrat, sans-serif;
}
</style>
