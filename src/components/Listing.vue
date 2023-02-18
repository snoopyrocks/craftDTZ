<template>
  <div v-if="nav !== 'repair'">
    <nav class="navbar navbar-expand-lg navbar-dark bg-black">
      <div class="container-fluid">
        <div id="navbarNav">
          <ul class="navbar-nav">
            <li
                @click="selectedCategory = key"
                v-for="(category, key) in categories" :key="key" class="nav-item">
              <a  class="nav-link" :class="{'active': selectedCategory === key}" href="#">{{ key.toUpperCase() }}</a>
            </li>
          </ul>
        </div>

      </div>

    </nav>
    <div class="content">
      <div class="list-group h-100 overflow-auto">
        <a href="#" @click="selectedItem = item[0]"
           :class="{'active': selectedItem === item[0]}"
           v-for="(item, key) in categories[selectedCategory]" :key="key"  class="list-group-item list-group-item-action flex-column align-items-start">
          <div class="d-flex w-100 justify-content-between">
            <h5 class="mb-1">{{trad[item[0]]}}</h5>
            <div>
              <span class="badge badge-pill bg-primary me-2">Level {{item[1].Level}}</span>
              <span class="badge badge-pill bg-primary">{{item[1].xp}}xp</span>
            </div>
          </div>
          <div class="d-flex flex-row">
            <button v-for="(key, val) in item[1].Ingredients" class="btn btn-outline-secondary me-2">{{ key }} {{trad[val]}}</button>
          </div>
        </a>
      </div>
    </div>
  </div>

  <div v-if="nav === 'repair'">
    <nav class="navbar navbar-expand-lg navbar-dark bg-black">
      <div class="container-fluid">
        <div id="navbarNav">
          <ul class="navbar-nav">
            <template v-for="(category, key) in all.repair" :key="key">
              <li
                  class="nav-item"
                  @click="selectedCategory = key">
                <a  class="nav-link" :class="{'active': selectedCategory === key}" href="#">{{ key.toUpperCase() }}</a>
              </li>
            </template>
          </ul>
        </div>

      </div>

    </nav>
    <div class="content">
      <div class="list-group h-100 overflow-auto">
        <a href="#" @click="selectedItem = item"
           :class="{'active': selectedItem === item}"
           v-for="(item, key) in all.repair[selectedCategory]" :key="key"  class="list-group-item list-group-item-action flex-column align-items-start">

          <div  class="d-flex w-100 justify-content-between">
            <h5 class="mb-1">{{item.label}}</h5>
            <div>
              <span class="badge badge-pill bg-primary me-2">Durabilité : {{item.durability}}</span>
              <span class="badge badge-pill bg-primary">Efficacité : {{ item.power}}</span>
              <span  v-if="item.traction" class="badge badge-pill bg-primary ms-2">Traction : {{ item.traction}}</span>
              <span  v-if="item.lowspeedtraction" class="badge badge-pill bg-primary ms-2">Traction démarrage : {{ item.lowspeedtraction}}</span>
              <span  v-if="item.shiftingtime" class="badge badge-pill bg-primary ms-2">Shiftingtime : {{ item.shiftingtime}}</span>
              <span  v-if="item.height" class="badge badge-pill bg-primary ms-2">Hauteur de caisse : {{ item.height}}</span>
            </div>
          </div>
          <div class="d-flex flex-row">
            <button v-for="(key, val) in item.repair" class="btn btn-outline-secondary me-2">{{ key.amount }} {{key.label}}</button>
          </div>
        </a>
      </div>
    </div>
  </div>


</template>

<script>
import buildings from "./../datas/buildings.json"
import mechanics from "./../datas/mechanics.json"
import fishing from "./../datas/fishing.json"
import cooking from "./../datas/cooking.json"
import repair from "./../datas/repair.json"
import correspondance from "./../datas/correspondance.json"
import forge from "./../datas/forge.json"
export default {
  props: {nav: String},
  data() {
    return {
      trad: correspondance,
      selectedCategory: "utility",
      selectedItem: "",
      all: {
        buildings,
        mechanics,
        fishing,
        cooking,
        repair,
        forge
      }
    }
  },
  computed: {
    categories(){
      const cat = this.all[this.nav]
      const sorted =  Object.entries(cat)
      .sort(([,a],[,b]) => a.Level-b.Level)
      // .reduce((r, [k, v]) => ({ ...r, [k]: v }), {});

      const grouped = sorted.reduce((groups, item) => ({
        ...groups,
        [item[1].Category]: [...(groups[item[1].Category] || []), item]
      }), {});
      this.selectedCategory = grouped[0]
      return grouped

    }
  }
}
</script>

