<template>


  <h1>PRODUCT CATALOG</h1>

  <div class="row">

  <div class="q-pa-md q-gutter-md" v-for="(item) in products" :key="item.id + 'products'">
    <div class="col-2">
      <ProductCard
        :id="item.id"  
        :name="item.title"
        :rating="item.rating.rate"
        :price="item.price"
        :image="item.image"/>
        
    </div>
  </div>
</div>



</template>





<script setup>

import ProductCard from "components/ProductsCard.vue"
import { inject, onMounted, ref } from "vue";

let products = ref([])


const fakecart = inject("fakestoreapi")





onMounted(async ()=>
{
  const result = await fakecart.get("/products")

console.log("MY PRODUCTS",result.data)

  products.value = result.data
})



</script>
