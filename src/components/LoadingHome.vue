<template>
  <div class="loading-home">
    <div class="container">
      <div class="text">
      Loading characters!
      </div>
      <PulseLoader :color="color"/>
    </div>
  </div>
</template>

<script>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

export default {
  name: 'LoadingHome',
  components: {
    PulseLoader
  },
  data() {
    return {
      color: "#FFE81F",
    }
  },
  methods: {

  }
}
</script>

<style scope lang="scss">
  .loading-home {
    & .container {
      padding-top: 200px;
    }
    & .text {
      padding: 20px;
      font-size: 30px;
    }
  }
</style>
