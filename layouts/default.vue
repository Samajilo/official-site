<template>
  <v-app>
    <v-main>
      <v-container
        fill-height
        fluid
        class="ma-0"
      >
        <div v-if="loading == false">
          <transition
            name="fade"
            mode="out-in"
          >
            <nuxt />
          </transition>
        </div>
        <v-row
          align="center"
          height="100%"
          justify="center"
          v-else
        >
          <div class="sk-wave">
            <div class="sk-wave-rect"></div>
            <div class="sk-wave-rect"></div>
            <div class="sk-wave-rect"></div>
            <div class="sk-wave-rect"></div>
            <div class="sk-wave-rect"></div>
          </div>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import 'spinkit/spinkit.min.css'

export default {
  name: 'indexPage',
  data () {
    return {
      loading: true
    }
  },
  beforeCreate () {
    setTimeout(() => { this.loading = false }, 2 * 1000)
    this.$router.beforeEach((to, from, next) => {
      this.loading = true
      next()
    })
    this.$router.afterEach(() => {
      setTimeout(() => { this.loading = false }, 0.5 * 1000)
    })
  }
}
</script>
<style>
  .palatinoFont {
    font-family: 'Palatino Linotype', sans-serif;
    font-size: 1.25rem;
  }
.fade-enter-active,
.fade-leave-active {
  transition-duration: 1s;
  transition-property: opacity;
  transition-timing-function: ease;
}

.fade-enter,
.fade-leave-active {
  opacity: 0
}
</style>
