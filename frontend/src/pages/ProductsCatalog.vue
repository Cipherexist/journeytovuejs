<template>


<h3>PRODUCT CATALOG</h3>

<div class="q-pa-md">
  <ProductCard name="French fries" rating="3" price="800"/>
</div>


</template>





<script setup>

import ProductCard from "components/ProductsCard.vue"
import { inject, ref } from "vue";

let products = ref([])


const fakecart = inject("fakestoreapi")

products = fakecart.get("/products")

console.log(products)


</script>
