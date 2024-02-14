<template>




<div class="q-pa-lg">
    <div class="row">
      <h4>PRODUCT CATALOG</h4>
    </div>
    <div class="row">
      <q-input bg-color="white" outlined  label-color="black" v-model="component.searchbox" label="Search here" @change="showlogs" />
    </div>

    <div class="row">


        <div class="q-pa-md q-gutter-md" v-for="(item) in products" :key="item.id + 'products/'">
           <!-- {{ component.searchtext = item.title }} -->
          <div class="col-2" v-if="component.searchbox==''">

              <ProductCard
                :id="item.id"
                :name="item.title"
                :rating="item.rating.rate"
                :price="item.price"
                :image="item.image"
                @-clickaddtocart="Savetocart"/>
            </div>

            <div class="col-2" v-else-if="item.title.toLowerCase().includes(component.searchbox.toLowerCase())">
              <ProductCard
                :id="item.id"
                :name="item.title"
                :rating="item.rating.rate"
                :price="item.price"
                :image="item.image"
                @-clickaddtocart="Savetocart"/>
            </div>
        </div>
    </div>

</div>



</template>





<script setup>

const containstxt = computed(()=>{ component.searchbox.contains(component.searchtext)})

function showlogs()
{
  console.log("Show Logs", component.searchbox)
}
function Savetocart(data)
{
  console.log("SERVER RECIEVED",data)
}

import ProductCard from "components/ProductsCard.vue"
import { computed, inject, onMounted, reactive, ref } from "vue";

const component = reactive
(
  {
    searchbox: "",
    searchtext: ""
  }

)



let products = ref([])


const fakecart = inject("fakestoreapi")





onMounted(async ()=>
{
  const result = await fakecart.get("/products")
  console.log("MY PRODUCTS",result.data)

  products.value = result.data
})



</script>
