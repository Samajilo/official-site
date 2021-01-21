<template>
  <v-row align="center" justify="center" class="mb-10 ma-auto" style="margin-bottom: 200px!important;">
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
            discover our history
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
        y: -40,
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
