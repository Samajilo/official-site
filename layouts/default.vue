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
          <div class="loader">
            Loading...
          </div>
          <!-- <div class="sk&#45;wave"> -->
          <!--   <div class="sk&#45;wave&#45;rect"></div> -->
          <!--   <div class="sk&#45;wave&#45;rect"></div> -->
          <!--   <div class="sk&#45;wave&#45;rect"></div> -->
          <!--   <div class="sk&#45;wave&#45;rect"></div> -->
          <!--   <div class="sk&#45;wave&#45;rect"></div> -->
          <!-- </div> -->
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
    setTimeout(() => { this.loading = false }, 4 * 1000)
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
<style lang="scss" scoped>
$color-background: #eaecfa;
$color-loader: #ce4233;

.loader {
  width: 250px;
  height: 50px;
  line-height: 50px;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  font-family: helvetica, arial, sans-serif;
  text-transform: uppercase;
  font-weight: 900;
  color: $color-loader;
  letter-spacing: 0.2em;
  
  &::before, &::after {
    content: "";
    display: block;
    width: 15px;
    height: 15px;
    background: $color-loader;
    position: absolute;
    animation: load .7s infinite alternate ease-in-out;
  }
  
  &::before {
    top: 0;
  }
  
  &::after {
    bottom: 0;
  }
}

@keyframes load {
  0% { left: 0; height: 30px; width: 15px }
  50% { height: 8px; width: 40px }
  100% { left: 235px; height: 30px; width: 15px}
}
</style>
