<template>
<div class="jhoto">
  <section class="image-gallery">
    <div class="image" v-for="item in items" :key="item.id">
    <div v-if="item.region === jhoto">
    <!--item.region.includes === jhoto-->


    <h2>{{item.title}}</h2>
    <h1>{{item.region}}</h1>

    <img :src="item.path" />
    <h6>{{item.description}}</h6>
    </div>



    </div>
  </section>
</div>

</template>

<style scoped>
.image h2 {
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
}

.image img {
  width: 100%;
}

/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 4;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
}
</style>


<script>
// @ is an alias to /src
import axios from 'axios';


export default {
  name: 'Jhoto',

  data() {
  return {
   items: [],
   jhoto: "Jhoto",
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
      console.log(error);
    }
  },
}


}
</script>
