<template>
  <v-row
    align="center"
    justify="center"
    class="mb-10 ma-auto"
    height="100vh"
    style="margin-bottom: 200px!important;margin-top: 100px!important;"
  >
    <v-col cols="auto" md="6">
      <v-hover
        v-slot="{ hover }"
      >
        <v-card
          :elevation="hover ? 12 : 3"
          class="pa-10 palatinoFont mt-20 animateCard"
        >
          <v-card-title class="title animateThis">
            We create 360<sup>o</sup> &nbsp; value by embrasing change.
          </v-card-title>
          <v-card-text>
            <div class="description animateThis">
              We now work with 91 of the Fortune Global 100. As of 2020, we've made
              18 consecutive appearances on the list of Fortune's "World's Most
              Admired Companies". And that's just the beginning.
            </div>
          </v-card-text>
          <v-card-actions class="justify-center link animateThis">
            <!-- discover our history -->
            <a href="#" class="btn-animate">
              <svg>
                <rect class="shape" height="50" width="200" />
              </svg>
              <span>discover our history</span>
            </a>
          </v-card-actions>
        </v-card>
      </v-hover>
    </v-col>
  </v-row>
</template>

<script>
import { gsap } from 'gsap/dist/gsap'
import ScrollTrigger from 'gsap/dist/ScrollTrigger'

export default {
  mounted () {
    gsap.registerPlugin(ScrollTrigger)
    const content = '.animateThis'
    gsap.fromTo(
      '.animateCard',
      {
        opacity: 0
      },
      {
        opacity: 1,
        duration: 3,
        ease: 'elastic',
        y: -20,
        scrollTrigger: {
          trigger: content,
          scrub: 0.5
        }
      }
    )
    gsap.fromTo(content,
      { opacity: 0 },
      {
        opacity: 1,
        duration: 3,
        y: -30,
        scrollTrigger: {
          trigger: content,
          scrub: 0.5
        }
      })
  }
}
</script>

<style scoped>
.title{
  font-size: 1.75rem!important;
}
.description {
  font-family: 'Palatino Linotype', sans-serif;
  font-size: 1.50rem!important;
}
.link {
  font-size: 1.30rem!important;
}
</style>
<style lang="scss" scoped>
$primary: #1976D2;
$filling_primary: #358ade;
$fs:'Lato', sans-serif;
$base: #000000;
$bg: #1976D2;
$w: 200px;
$h: 50px;
$blue: #19B5FE;
p{
  font-family:$fs;
  color:darken( $base, 30% )
}
.btn-animate {
  text-decoration: none;
  font-family: $fs;
  color: #FFF;
  position: relative;
  display: inline-block;
  margin: 0 auto;
  width: $w;
  height: $h;
  overflow: hidden;
  >svg {
    position:absolute;
    top:0;
    left:0;
    width:$w;
    height:$h;
    stroke-width:8px;
    stroke:$base;
    stroke-linecap:round;
    fill:transparent;
  }
  >span {
    color: $base;
    width: $w;
    height: $h;
    display: inline-block;
    text-align:center;
    font-size:20px;
    position:absolute;
    left:0;
    top:0;
    line-height:2.3;
    transition:all .2s ease;
    &:after {
      position:absolute;
      content:"Let's GO!";
      color:white!important;
      top:0;
      left:-100%;
      width:$w;
      height:$h;
      color: $bg;
      transition:all .2s ease;
    }
    &:before{
      position:absolute;
      content:'';
      height:$h;
      z-index:0;
      width:$h;
      background-color:$base;
      border-radius:50%;
      top:0;
      left:-63%;
      transition:all .4s ease;
      transform:scale(0);
      opacity:0;
    }
  }
  &:hover > svg {
    transition-delay: 250ms;
    background-color: fade(black, 40%);
    color: white;
    animation: 1s pencil linear forwards;
  }
  &:hover > span {
    left:100%;
  }
  &:hover > span:after {
    left:-100%;
  }
}
@keyframes pencil {
  0% {
    stroke-dasharray: 300;
    stroke-dashoffset: 700;
    stroke-width: 8px;
  }
  75% {
    stroke-dasharray: 900;
    stroke-dashoffset: 400;
    stroke-width: 1px;
    fill: $filling_primary;
  }
  100% {
    stroke-dasharray: 900;
    stroke-dashoffset: 400;
    stroke-width: 1px;
    fill: $primary;
  }
}
</style>
