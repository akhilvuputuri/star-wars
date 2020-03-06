<template>
  <div>
    <div class="header">Star Wars Wiki</div>
    <div v-if="showProfiles && !isFetchingHome" class="people">
      <div v-bind:key="person.id" v-for="(person, index) in people">
        <button class="button" v-on:click="loadProfile(index)">
          <PersonCard v-bind:person="person" />
        </button>
      </div>
    </div>
    <div v-if="showProfiles && isFetchingHome">
      <LoadingHome />
    </div>
    <div v-else-if="!showProfiles && !isFetching">
      <PersonProfile
      v-bind:profile="people[selectedProfileIndex]"
      @showAllProfiles="showAllProfiles()"
      />
    </div>
    <div v-else-if="!showProfiles && isFetching">
      <LoadingProfile
      v-bind:profile="people[selectedProfileIndex]"
      />
    </div>
  </div>
</template>

<script>
import PersonCard from "./PersonCard"
import PersonProfile from "./PersonProfile"
import LoadingProfile from "./LoadingProfile"
import LoadingHome from "./LoadingHome"
import axios from "axios";

export default {
  name: 'People',
  components: {
    PersonCard,
    PersonProfile,
    LoadingProfile,
    LoadingHome
  },
  data() {
    return {
      showProfiles: true,
      people: [],
      isFetchingHome: false,
      isFetching: false,
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
      if (!this.isCached(index)) {
        this.fetchAndCache(index)
      }
      this.selectedProfileIndex = index
    },
    isCached(personIndex) {
      if (this.people[personIndex].isCached) {
        console.log("Is cached!")
        return true
      } else {
        console.log("NOT cached!")
        return false
      }
    },
    fetchAndCache(personIndex) {
      this.isFetching = true
      var fetchArr = [false, false, false, false, false]
      // homeworld
      var homeworld = this.people[personIndex].homeworld
      if (homeworld.includes("https")) {
        fetchArr[0] = true
        axios.get(homeworld)
        .then(res => {
          this.people[personIndex].homeworld = res.data.name
          fetchArr[0] = false
          console.log(fetchArr)
          this.isFetching = fetchArr[0] || fetchArr[1] || fetchArr[2] || fetchArr[3] || fetchArr[4]
          })
        .catch(err => console.log(err))
      }
      // films
      var films = this.people[personIndex].films
      var countFilms = films.length
      for (var i = 0; i < films.length; i++) {
        console.log("i: " + i)
        const index = i // set index as i changes before get request data is returned
        if (films[index].includes("https")) {
          fetchArr[1] = true
          axios.get(films[index])
          .then(res => {
            films[index] = res.data.title
            countFilms--
            if (countFilms == 0) {
              fetchArr[1] = false
            }
            console.log(fetchArr)
            this.isFetching = fetchArr[0] || fetchArr[1] || fetchArr[2] || fetchArr[3] || fetchArr[4]
            })
          .catch(err => console.log(err))
        }
      }
      // species
      var species = this.people[personIndex].species
      var countSpecies = species.length
      for (var j = 0; j < species.length; j++) {
        const index = j // set index as i changes before get request data is returned
        if (species[index].includes("https")) {
          fetchArr[2] = true
          axios.get(species[index])
          .then(res => {
            species[index] = res.data.name
            countSpecies--
            if (countSpecies == 0) {
              fetchArr[2] = false
            }
            console.log(fetchArr)
            this.isFetching = fetchArr[0] || fetchArr[1] || fetchArr[2] || fetchArr[3] || fetchArr[4]
            })
          .catch(err => console.log(err))
        }
      }
      // vehicles
      var vehicles = this.people[personIndex].vehicles
      var countVehicles = vehicles.length // count requests done for this for loop
      for (var k = 0; k < vehicles.length; k++) {
        const index = k // set index as i changes before get request data is returned
        if (vehicles[index].includes("https")) {
          fetchArr[3] = true
          axios.get(vehicles[index])
          .then(res => {
            vehicles[index] = res.data.name
            countVehicles--
            if (countVehicles == 0) {
              fetchArr[3] = false
            }
            console.log(fetchArr)
            this.isFetching = fetchArr[0] || fetchArr[1] || fetchArr[2] || fetchArr[3] || fetchArr[4]
            })
          .catch(err => console.log(err))
        }
      }
      // starships
      var starships = this.people[personIndex].starships
      var countStarships = starships.length
      for (var l = 0; l < starships.length; l++) {
        const index = l // set index as i changes before get request data is returned
        if (starships[index].includes("https")) {
          fetchArr[4] = true
          axios.get(starships[index])
          .then(res => {
            starships[index] = res.data.name
            countStarships--
            if (countStarships == 0) {
              fetchArr[4] = false
            }
            console.log(fetchArr)
            this.isFetching = fetchArr[0] || fetchArr[1] || fetchArr[2] || fetchArr[3] || fetchArr[4]
            })
          .catch(err => console.log(err))
        }
      }
      this.people[personIndex].isCached = true
    }
  },
  created() {
    this.isFetchingHome = true
    axios.get('https://swapi.co/api/people/')
      .then(res => {
        this.people = res.data.results
        console.log(this.people)
        this.isFetchingHome = false
        })
      .catch(err => console.log(err))
  }
}
</script>

<style scoped lang="scss">
.header {
  font-size: 40px;
  font-weight: bold;
  color: #FFE81F;
  background-color: black;
  padding: 10px;
  margin-bottom: 10px;
}
.people {
  width: 50%;
  margin: 0 auto;
  & .button {
    color: black;
    background-color: white;
    font-size: 32px;
    border: 1px solid black;
    border-radius: 5px;
    margin: 10px;
    cursor: pointer;
  }
  & .button:hover {
      color: #FFE81F;
      background-color: black;
      border: 1px solid #FFE81F;
    }
}
</style>
