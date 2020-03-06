<template>
  <div class="person-card">
    <div>Name: {{person.name}}</div>
    <div>Height: {{person.height}}</div>
    <div>Mass: {{person.mass}}</div>
    <div>Hair Color: {{person.hair_color}}</div>
    <div>Skin Color: {{person.skin_color}}</div>
    <div>Eye Color: {{person.eye_color}}</div>
    <div>Birth Year: {{person.birth_year}}</div>
    <div>Gender: {{person.gender}}</div>
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
