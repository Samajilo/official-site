<template>
  <div>
    <div>
      <v-main>
        <HomePhoto />
        <DiscoverHistoryLink />
      </v-main>
    </div>
  </div>
</template>

<script>
import HomePhoto from '../components/HomePhoto'
import DiscoverHistoryLink from '../components/DiscoverHistoryLink'

export default {
  name: 'indexPage',
  components: {
    HomePhoto,
    DiscoverHistoryLink
  },
  data () {
    return {
    }
  }
}
</script>
<style scoped>
</style>
