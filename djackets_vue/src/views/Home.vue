<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">Welcome to Djackets</p>
        <p class="subtitle">The best Shoe and Jacket online store</p>
      </div>
    </section>
    <div class="column is-multiline">
    <div class="column is-12">
      <h2 class="is-size-2 has-text-centered">
        Latest Products
      </h2>
    </div>
    <ProductBox
    v-for="product in latestProducts"
    v-bind:key="product.id"
    v-bind:product="product"/>
  </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import ProductBox from '@/components/ProductBox'

export default {
  name: "Home",
  data(){
    return {
      latestProducts:[]
    }
  },
  components: {
    ProductBox
  },
  mounted(){
    this.getLatestProducts()
    document.title='Home | Djackets'
  },
  methods:{
    getLatestProducts(){
      axios.get('/api/v1/latest-products/')
      .then((response)=>{
        this.latestProducts=response.data
      })
      .catch(error=>{
        console.log(error)
      })
    }
  }
};
</script>
