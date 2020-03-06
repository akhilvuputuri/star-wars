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
        <PersonProfile v-bind:profile="people[selectedProfileIndex]" />
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
    loadProfile(index) {
      console.log("clicked")
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
      console.log(this.people[personIndex].films)
      // species
      // vehicles
      // starships
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
