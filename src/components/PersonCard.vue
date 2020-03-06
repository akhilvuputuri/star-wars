<template>
  <div class="person-card">
    <div>{{person.name}}</div>
  </div>
</template>

<script>
// import axios from "axios";

export default {
  name: 'PersonCard',
  props: ["person"],
  components: {

  },
  data() {
    return {
    }
  },
  methods: {

  },
  created() {

  }
}
</script>

<style scoped>
  .people-card {
    flex: 1;
  }
</style>
