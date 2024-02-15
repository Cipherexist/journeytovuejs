
<style scoped>

.my-card
{
  width: 700px;
  max-width: 80vw;
  max-width: 50px;
  max-height: auto;
  height: auto;
}

.imgitem
{
  max-width: 180px;
  height: 220px;
  object-fit: scale-down;
}


</style>

<script setup>

const props = defineProps(
  {
    title:
    {
      required: true,
      type: String
    },
    description:
    {
      required: true,
      type: String
    },
    image:
    {
      required: true,
      type: String
    },
    price:
    {
      required: true,
      type: Number
    }
  })


</script>

<template>

<q-card class="my-card q-pa-md">
      <q-img class="imgitem" :src="props.image" fit="fill">
        <div class="absolute-bottom text-h6">
          {{ props.title }}
        </div>
      </q-img>

      <q-card-section>
        {{ props.description }}
      </q-card-section>
</q-card>


</template>
