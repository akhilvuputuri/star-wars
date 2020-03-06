<template>
  <div id="person-profile">
    Person's profile
    <button v-on:click="hideProfile()">Hide Profile</button>
  </div>
</template>

<script>

export default {
  name: 'PersonProfile',
  props: ["profile"],
  components: {
    
  },
  data() {
    return {

    }
  },
  methods: {
    hideProfile() {
      console.log(this.profile)
      this.$emit('showAllProfiles', true)
    }
  }
}
</script>

<style>

</style>
