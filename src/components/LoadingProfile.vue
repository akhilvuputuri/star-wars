<template>
  <div id="loading-profile">
    <div>
      Loading {{this.profile.name}}'s profile!
    </div>
    <PulseLoader />
  </div>
</template>

<script>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

export default {
  name: 'LoadingProfile',
  props: ["profile"],
  components: {
    PulseLoader
  },
  data() {
    return {

    }
  },
  methods: {

  }
}
</script>

<style>

</style>
