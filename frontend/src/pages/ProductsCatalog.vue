<style scoped>

.my-card
{
  max-width: 450px;
  height: 450px;
}
.img
{
  margin-top: 20px;
  max-width: 150px;
  height: 150px;
}

</style>


<template>


<q-layout>
  <q-page-container>
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
                      :description="item.description"
                      :image="item.image"
                      @-clickaddtocart="Savetocart"/>
                  </div>

                  <div class="col-2" v-else-if="item.title.toLowerCase().includes(component.searchbox.toLowerCase())">
                    <ProductCard
                      :id="item.id"
                      :name="item.title"
                      :rating="item.rating.rate"
                      :price="item.price"
                      :description="item.description"
                      :image="item.image"
                      @-clickaddtocart="Savetocart"/>
                  </div>
              </div>
          </div>

      </div>

      <q-page-sticky position="bottom-right" :offset="[18, 18]">
            <q-btn fab icon="shopping_cart" color="positive" />
          </q-page-sticky>
  </q-page-container>
</q-layout>

<q-dialog v-model="icon">
  <q-card class="my-card">
    <div class="q-pa-md ">
      <q-img class="img" :src="component.popupimage" fit="fill" />


    </div>
    <q-card-section>

          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis">
             {{ component.popuptitle }}
            </div>

          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-subtitle1">
           ${{ component.popupprice }}
          </div>
          <div class="text-caption text-grey">
            {{ component.popupdescription }}
          </div>
        </q-card-section>

        <q-separator />

        <q-card-actions align="right">
          <q-btn v-close-popup flat color="primary" label="Add to Cart" round icon="shopping_cart" />
        </q-card-actions>
      </q-card>
</q-dialog>







</template>





<script setup>

const containstxt = computed(()=>{ component.searchbox.contains(component.searchtext)})

function showlogs()
{
  console.log("Show Logs", component.searchbox)

}


function Savetocart(data)
{

  console.log("SERVER ID",data.id)
  console.log("SERVER NAME",data.name)
  component.popuptitle = data.name
  component.popupimage = data.image
  component.popupprice = data.price
  component.popupdescription = data.description
  icon.value = true
}

import ProductCard from "components/ProductsCard.vue"
import {computed, inject, onMounted, reactive, ref } from "vue";




const icon = ref(false)

const component = reactive
(
  {
    searchbox: "",
    searchtext: "",
    popuptitle: "",
    popupdescription: "",
    popupimage: "",
    popupprice: ""
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
