<template>
  <div>
    <div v-if="loading == false">
      <v-main>
        <transition
          name="fade"
          mode="out-in"
        >
          <div>
            <HomePhoto />
            <DiscoverHistoryLink />
          </div>
        </transition>
      </v-main>
    </div>
    <v-container
      fill-height
      fluid
      v-else
    >
      <v-row
        align="center"
        height="100vh"
        justify="center"
      >
        <client-only>
          <spring-spinner
            :animation-duration="3000"
            :size="60"
            color="blue"
          />
        </client-only>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { SpringSpinner } from 'epic-spinners'
import HomePhoto from '../components/HomePhoto'
import DiscoverHistoryLink from '../components/DiscoverHistoryLink'

export default {
  name: 'indexPage',
  components: {
    HomePhoto,
    DiscoverHistoryLink,
    SpringSpinner
  },
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
<style scoped>
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
