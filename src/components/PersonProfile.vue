<template>
  <div id="person-profile">
    Person's profile
    <button v-on:click="hideProfile()">Hide Profile</button>
  </div>
</template>

<script>

export default {
  name: 'PersonProfile',
  props: ["profile", "showProfiles"],
  components: {
    
  },
  data() {
    return {

    }
  },
  methods: {
    hideProfile() {
      console.log("Trigger from profile")
      this.$emit('showAllProfiles', true)
    }
  }
}
</script>

<style>

</style>
