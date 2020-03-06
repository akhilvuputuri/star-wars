<template>
  <div id="person-profile">
    <div>Person's profile</div>
    <div>Name: {{profile.name}}</div>
    <div>Height: {{profile.height}}</div>
    <div>Mass: {{profile.mass}}</div>
    <div>Hair Color: {{profile.hair_color}}</div>
    <div>Skin Color: {{profile.skin_color}}</div>
    <div>Eye Color: {{profile.eye_color}}</div>
    <div>Birth Year: {{profile.birth_year}}</div>
    <div>Gender: {{profile.gender}}</div>
    <div>Homeworld: {{profile.homeworld}}</div>
    <div>FILMS:</div>
    <div v-bind:key="film" v-for="film in profile.films">
        <div>{{film}}</div>
    </div>
    <div>SPECIES:</div>
    <div v-bind:key="specie" v-for="specie in profile.species">
        <div>{{specie}}</div>
    </div>
    <div>VEHICLES:</div>
    <div v-bind:key="vehicle" v-for="vehicle in profile.vehicles">
        <div>{{vehicle}}</div>
    </div>
    <div>STARSHIPS:</div>
    <div v-bind:key="starship" v-for="starship in profile.starships">
        <div>{{starship}}</div>
    </div>
    <div>
      <button v-on:click="hideProfile()">Hide Profile</button>
    </div>
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
