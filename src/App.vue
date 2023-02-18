<script>
import Listing from './components/Listing.vue'

const navs = {
  buildings: "Buildings",
  mechanics: "Mécanique",
  fishing: "Pêche / Chasse",
  cooking: "Cuisine",
  repair: "Réparation véhicule",
}
export default {
  components: {
    Listing
  },
  data(){
    return {
      navs,
      nav: "buildings"
    }
  },
}


</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-black">
    <div class="container-fluid">

      <div id="navbarNav">
        <ul class="navbar-nav">
          <li
              @click="nav = key"
              v-for="(navigation, key) in navs" :key="key" class="nav-item">
            <a  class="nav-link" :class="{'active': nav === key}" href="#">{{ navigation }}</a>
          </li>
        </ul>
      </div>
    </div>

  </nav>
  <Listing :nav="nav" />

</template>
