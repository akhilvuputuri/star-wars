<template>
  <div>
    <div class="person-profile">
      <div>
        <button class="button" v-on:click="hideProfile()">Back</button>
      </div>
      <div class="name">{{profile.name}}</div>
      <div>
        <div class="personal-information box-border">
          <div class="title">Personal Info:</div>
          <div>Height: {{profile.height}}</div>
          <div>Mass: {{profile.mass}}</div>
          <div>Hair Color: {{profile.hair_color}}</div>
          <div>Skin Color: {{profile.skin_color}}</div>
          <div>Eye Color: {{profile.eye_color}}</div>
          <div>Birth Year: {{profile.birth_year}}</div>
          <div>Gender: {{profile.gender}}</div>
          <div>Homeworld: {{profile.homeworld}}</div>
        </div>
      </div>
      <div class="row">
        <div class="column">
          <div class="films box-border">
            <div class="title">Films:</div>
            <div v-if="profile.films.length > 0">
              <div v-bind:key="film" v-for="film in profile.films">
                {{film}}
              </div>
            </div>
            <div v-else>
              NONE
            </div>
          </div>
        </div>
        <div class="column">
          <div class="species box-border">
            <div class="title">Species:</div>
            <div v-if="profile.species.length > 0">
              <div v-bind:key="specie" v-for="specie in profile.species">
                {{specie}}
              </div>
            </div>
            <div v-else>
              NONE
            </div>
          </div>
          <div class="vehicles box-border">
            <div class="title">Vehicles:</div>
            <div v-if="profile.vehicles.length > 0">
              <div v-bind:key="vehicle" v-for="vehicle in profile.vehicles">
                {{vehicle}}
              </div>
            </div>
            <div v-else>
              NONE
            </div>
          </div>
          <div class="starships box-border">
            <div class="title">Starships:</div>
            <div v-if="profile.starships.length > 0">
              <div v-bind:key="starship" v-for="starship in profile.starships">
                {{starship}}
              </div>
            </div>
            <div v-else>
              NONE
            </div>
          </div>
        </div>
      </div>
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
      this.$emit('showAllProfiles', true)
    }
  }
}
</script>

<style scoped lang="scss">
  .person-profile {
    width: 30%;
    margin: 0 auto;
    font-size: 24px;
    & .row {
      display: flex;
    }
    & .column {
      flex: 1;
    }
    & .button {
      color: black;
      background-color: white;
      font-size: 30px;
      border: 1px solid black;
      border-radius: 5px;
      cursor: pointer;
    }
    & .button:hover {
      color: #FFE81F;
      background-color: black;
      border: 1px solid #FFE81F;
    }
    & .name {
      font-size: 40px;
      font-weight: bold;
      margin: 10px;
    }
    & .box-border {
      border: 1px solid #000;
      margin: 10px;
    }
    & .title {
      font-size: 28px;
      font-weight: bold;
      text-decoration: underline;
    }
  }
</style>
