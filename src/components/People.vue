<template>
  <div>
    <div v-if="showProfiles" class="people">
      <div v-bind:key="person.id" v-for="(person, index) in people">
        <button v-on:click="loadProfile(index)">
          <PersonCard v-bind:person="person" />
        </button>
      </div>
    </div>
    <div v-else-if="!showProfiles" class="person-profile">
        <PersonProfile
        v-bind:profile="people[selectedProfileIndex]"
        v-bind:showProfiles="showProfiles"
        @showAllProfiles="showAllProfiles()"
        />
    </div>
  </div>
</template>

<script>
import PersonCard from "./PersonCard"
import PersonProfile from "./PersonProfile"
import axios from "axios";

export default {
  name: 'People',
  components: {
    PersonCard,
    PersonProfile
  },
  data() {
    return {
      showProfiles: true,
      people: [],
      selectedProfileIndex: 0,
    }
  },
  methods: {
    showAllProfiles() {
      console.log("Hello world")
      this.showProfiles = true
    },
    loadProfile(index) {
      this.showProfiles = false
      this.fetchAndCache(index)
      this.selectedProfileIndex = index

    },
    fetchAndCache(personIndex) {
      // films
      var films = this.people[personIndex].films
      for (var i = 0; i < films.length; i++) {
        console.log("i: " + i)
        const index = i // set index as i changes before get request data is returned
        if (films[index].includes("https")) {
          axios.get(films[index])
          .then(res => {
            console.log(res.data.title)
            films[index] = res.data.title
            console.log(films)
            })
          .catch(err => console.log(err))
        }
      }
      // species
      var species = this.people[personIndex].species
      for (var j = 0; j < species.length; j++) {
        const index = j // set index as i changes before get request data is returned
        if (species[index].includes("https")) {
          axios.get(species[index])
          .then(res => {
            species[index] = res.data.name
            console.log(species)
            })
          .catch(err => console.log(err))
        }
      }
      // vehicles
      var vehicles = this.people[personIndex].vehicles
      for (var k = 0; k < vehicles.length; k++) {
        const index = k // set index as i changes before get request data is returned
        if (vehicles[index].includes("https")) {
          axios.get(vehicles[index])
          .then(res => {
            vehicles[index] = res.data.name
            console.log(vehicles)
            })
          .catch(err => console.log(err))
        }
      }
      // starships
      var starships = this.people[personIndex].starships
      for (var l = 0; l < starships.length; l++) {
        const index = l // set index as i changes before get request data is returned
        if (starships[index].includes("https")) {
          axios.get(starships[index])
          .then(res => {
            starships[index] = res.data.name
            console.log(starships)
            })
          .catch(err => console.log(err))
        }
      }
    }
  },
  created() {
    axios.get('https://swapi.co/api/people/')
      .then(res => {
        this.people = res.data.results
        console.log(this.people)
        })
      .catch(err => console.log(err))
  }
}
</script>

<style scoped>
.people {
  display: flex;
}
</style>
