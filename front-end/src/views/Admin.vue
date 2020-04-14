<template>
<div class="admin">
  <div v-if="this.databaseSize >= 6" style="font-size: 30px; background: #4caf50; border: 4px solid #000000; padding: 16px; width: 98.5%; min-width: 580px; text-align:center; "  ><strong> 
    You have maxed out your team with 6 Pokemon! Please remove a Pokemon if you wish to add a different one.
  </strong></div>

  <br>
 
  <div class="columns">
    <div class="column-container">
      <h1>Team Builder</h1>
      <div class="form">
        <input v-model="findTitle" placeholder="Search">
        <div class="suggestions" v-if="suggestions.length > 0">
          <div class="suggestion" v-for="s in suggestions" :key="s.id" @click="selectItem(s)">
            {{s.name}} 
          </div>
        </div>
      </div>
    </div>
    <div class="column-container">
      <section class="image-gallery"  >
        <div class="image" v-for="item in databaseItems" :key="item._id" style="border: 1px solid #333; padding:10px;" >
          <h2>{{item.name}}</h2>
          <img :src="'/images/pokemon_images/' + item.path" />
          <div>{{item.desc}}</div>
          <button @click="deleteItem(item)">Remove</button>
        </div>
      </section>
    </div>
  </div>
</div>
</template>

<script>

import axios from 'axios';
import pokemons from '../pokemons.js'

export default {
  name: 'Admin',
  data() {
    return {
      title: "",
      file: null,
      addItem: null,
      items: [],
      databaseItems: [],
      findTitle: "",
      findItem: null,
      firstTextArea: "",
      databaseSize: 0,
    }
  },
  computed: {
    suggestions() {
      let items = this.items.filter(item => item.name.toLowerCase().includes(this.findTitle.toLowerCase()));
      return items.sort((a, b) => a.name > b.name);
    }
  },
  created() {
    this.items = pokemons;
    this.getItems();
  },
  methods: {
    fileChanged(event) {
      this.file = event.target.files[0]
    },
    async selectItem(item) {
      if(this.databaseSize >= 6){
        return;
      }
      try {
        let r2 = await axios.post('/api/items', {
          id:	item.id,
          name: item.name,
          type1: item.type1,
          type2: item.type2,
          total: item.total, 
          hp:	item.hp,
          attack:	item.attack,
          defense:	item.defense,
          spatk:	item.spatk,
          spdef:	item.spdef,
          sp:	item.sp,
          path: item.image,
        });
        this.addItem = r2.data;
        this.getItems();
      } catch (error) {
        console.log("error!");
        return;
      }
    },
    async getItems() {
      try {
        let response = await axios.get("/api/items");
        this.databaseItems = response.data;
        this.databaseSize = this.databaseItems.length;
        return true;
      } catch (error) {
        return;
      }
    },
    async deleteItem(item) {
      try {
        await axios.delete("/api/items/" + item._id);
        this.findItem = null;
        this.getItems();
        return true;
      } catch (error) {
        return;
      }
    },
 },
}

</script>


<style scoped>
.image h2 {
  font-style: italic;
  font-size: 1em;
}

.heading {
  display: flex;
  margin-bottom: 20px;
  margin-top: 20px;
}

.heading h2 {
  margin-top: 8px;
  margin-left: 10px;
}

.add,
.edit {
  display: flex;
}

.circle {
  border-radius: 50%;
  width: 18px;
  height: 18px;
  padding: 8px;
  background: #333;
  color: #fff;
  text-align: center
}

/* Form */
input,
textarea,
select,
button {
  font-family: 'Montserrat', sans-serif;
  font-size: 1em;
}

.form {
 
}

/* Uploaded images */
.upload h2 {
  margin: 0px;
}

.upload img {
  max-width: 200px;
}

/* Suggestions */
.suggestions {
  width: auto;
  ;
  border: 1px solid #d7d7d7;
}

.suggestion {
  min-height: 20px;
}

.suggestion:hover {
  background-color: #4caf50 ;
  color: #fff;
}

.columns {
  display: grid;
  grid-gap: 25px;
  grid-template-columns: auto auto;
  background-color: #333333;
  padding: 10px;
  width: 100%;
  min-width: 580px;
}

.column-container {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 5px;
  font-size: 20px;
  text-align: center;
  width: 80%;
}

</style>
