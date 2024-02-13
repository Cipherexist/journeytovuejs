<template>


<h3>PRODUCT CATALOG</h3>

<div>
  <div class="q-pa-md" v-for="(item) in products" :key="item.id + 'products'">
    <ProductCard
    :name="item.title"
    :rating="item.rating.rate"
    :price="item.price"
    :image="item.image"/>
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
