<style scoped>
.my-card
{
  max-width: 230px;
  height: auto;
}
</style>

<script setup>
import { computed, ref } from 'vue';


const props = defineProps(
  {
    id:
    {
      required: true,
      type: String
    },
    name:
    {
      required: true,
      type: String
    },
    rating:
    {
      required: true,
      type: Number
    },
    price:
    {
      required: true,
      type: Number
    },
    image:
    {
      required: true,
      type: String
    },

  })

  function addtocart(id)
  {
    console.log("MYPRODUCTID", id)
  }


</script>


<template>

<q-card class="my-card" flat bordered>
      <q-img :src="props.image" :fit="fill"/>

      <q-card-section>
        <q-btn
          
          fab
          @click="addtocart(props.id)"
          color="primary"
          icon="place"
          class="absolute"
          style="top: 0; right: 12px; transform: translateY(-50%);"
        />

        <div class="row no-wrap items-center">
          <div class="col text-h6 ellipsis">
            {{props.name}}
          </div>

        </div>

        <q-rating v-model="ratingModel" :model-value="props.rating" :max="5" size="32px" />
      </q-card-section>

      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          ${{ props.price }}
        </div>

      </q-card-section>

      <q-separator />

      <q-card-actions>
        <q-btn flat round icon="event" />
        <q-btn flat color="primary">
          Reserve
        </q-btn>
      </q-card-actions>
    </q-card>

</template>
