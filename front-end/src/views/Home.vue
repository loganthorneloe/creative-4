<template>
<div class="home">
  <section class="image-gallery">
    <div class="image" v-for="item in items" :key="item._id">
      <h2>{{item.name}}</h2>
      <img :src="'/images/pokemon_images/' + item.path" />
      <div>{{item.desc}}</div>
      <div class="stat-box">
        <p><u>Pokemon Stats:</u></p>
        <p>Type: {{item.type1}} & {{item.type2}}</p>
        <div class="grid-container">
          <div class="grid-item">HP: {{item.hp}}</div>
          <div class="grid-item">Atk: {{item.attack}}</div>
          <div class="grid-item">Def: {{item.defense}}</div>  
          <div class="grid-item">Speed: {{item.sp}}</div>
          <div class="grid-item">Sp.Atk: {{item.spatk}}</div>
          <div class="grid-item">Sp.Def: {{item.spdef}}</div>  
        </div>
      </div>
    </div>
  </section>
</div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
export default {
  name: 'Home',
   data() {
    return {
     items: [],
    }
  },
  created() {
    this.getItems();
  },
  methods: {
    async getItems() {
      try {
        let response = await axios.get("/api/items");
        this.items = response.data;
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
  margin-top: 5px;
  margin-bottom: 0px;
  font-size: 20px;
  font-style: italic;
}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

.image-gallery {
  column-gap: 1.5em;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  width: 100%;

    border: 3px solid rgb(63, 85, 126);
    border-radius: 5px;
    margin: auto;
    text-align: center;
    margin-bottom: 15px;
}

.image img {
  width: 100%;
}

/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
  .grid-container {
    column-count: 2;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
  .grid-container {
    column-count: 1;
  }
}


.stat-box {
  background-color: #4caf50;
  padding-top: 2px;
}

.stat-box p {
  margin: 2px;
}


.grid-container {
  display: grid;
  grid-gap: 2px;
  grid-template-columns: auto auto auto;
  padding: 6px;
}

.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 6px;
  font-size: 10px;
  text-align: center;
}
</style>
