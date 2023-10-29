<script>
import ListingDTZ from './components/ListingDTZ.vue'
import ListingPulse from './components/ListingPulse.vue'

const navsDTZ = {
  mechanics: "Mécanique",
  repair: "Réparation véhicule",
  buildings: "Buildings",
  forge: "Forge",
  weapons: "Armes",
  fishing: "Pêche / Chasse",
  cooking: "Cuisine",
}

const navsPulse = {
  // mechanics: "Mécanique",
  // repair: "Réparation véhicule",
  buildings: "Buildings",
  // forge: "Forge",
  // weapons: "Armes",
  // fishing: "Pêche / Chasse",
  cooking: "Cuisine",
}
export default {
  components: {
    ListingDTZ,
    ListingPulse
  },
  data(){
    return {
      mainNav: "",
      navsDTZ,
      navsPulse,
      search: "",
      nav: "buildings"
    }
  },
}


</script>

<template>
  <template v-if="mainNav === ''">
    <div class="h-100 d-flex justify-content-center align-items-center flex-column">
      <button class="btn btn-primary mb-4 w-25" @click="mainNav = 'DTZ'">DTZ</button>
      <button class="btn btn-primary w-25" @click="mainNav = 'Pulse'">Pulse</button>
    </div>
  </template>
  <template v-if="mainNav === 'Pulse'">
    <nav class="navbar navbar-expand-lg navbar-dark bg-black">
      <div class="container-fluid">

        <div id="navbarNav" class="w-100 d-flex justify-content-between">
          <ul class="navbar-nav">
            <li class="nav-item" @click="mainNav= ''">
              <a class="nav-link fw-bold" href="#">Retour
              </a>
            </li>
            <li
                @click="nav = key"
                v-for="(navigation, key) in navsPulse" :key="key" class="nav-item">
              <a  class="nav-link fw-bold" :class="{'active': nav === key}" href="#">{{ navigation.toUpperCase() }}</a>
            </li>
          </ul>
          <div>
            <input v-model="search" type="text" class="form-control" placeholder="Recherche"/>
          </div>
        </div>
      </div>

    </nav>
    <ListingPulse :nav="nav" :search="search"/>
  </template>
  <template v-if="mainNav === 'DTZ'">
    <nav class="navbar navbar-expand-lg navbar-dark bg-black">
      <div class="container-fluid">

        <div id="navbarNav" class="w-100 d-flex justify-content-between">
          <ul class="navbar-nav">
            <li class="nav-item" @click="mainNav= ''">
              <a class="nav-link fw-bold" href="#">Retour
              </a>
            </li>
            <li
                @click="nav = key"
                v-for="(navigation, key) in navsDTZ" :key="key" class="nav-item">
              <a class="nav-link fw-bold" :class="{'active': nav === key}" href="#">{{ navigation.toUpperCase() }}</a>
            </li>
          </ul>
          <div>
            <input v-model="search" type="text" class="form-control" placeholder="Recherche"/>
          </div>
        </div>
      </div>

    </nav>
    <ListingDTZ :nav="nav" :search="search"/>
  </template>
</template>
