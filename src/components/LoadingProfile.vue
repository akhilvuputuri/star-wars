<template>
  <div id="loading-profile">
    Loading {{this.profile.name}}'s profile!
  </div>
</template>

<script>

export default {
  name: 'LoadingProfile',
  props: ["profile"],
  components: {
    
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
