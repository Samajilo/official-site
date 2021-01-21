<template>
  <div>
    <HomePhoto />
    <DiscoverHistoryLink />
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
  }
}
</script>
