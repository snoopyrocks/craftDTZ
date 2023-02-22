<script>
import Listing from './components/Listing.vue'

const navs = {
  mechanics: "Mécanique",
  repair: "Réparation véhicule",
  buildings: "Buildings",
  forge: "Forge",
  weapons: "Armes",
  fishing: "Pêche / Chasse",
  cooking: "Cuisine",
}
export default {
  components: {
    Listing
  },
  data(){
    return {
      navs,
      search: "",
      nav: "mechanics"
    }
  },
}


</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-black">
    <div class="container-fluid">

      <div id="navbarNav" class="w-100 d-flex justify-content-between">
        <ul class="navbar-nav">
          <li
              @click="nav = key"
              v-for="(navigation, key) in navs" :key="key" class="nav-item">
            <a  class="nav-link fw-bold" :class="{'active': nav === key}" href="#">{{ navigation.toUpperCase() }}</a>
          </li>
        </ul>
        <div>
          <input v-model="search" type="text" class="form-control" placeholder="Recherche"/>
        </div>
      </div>
    </div>

  </nav>
  <Listing :nav="nav" :search="search"/>

</template>
