<style scoped>
 h1 {
    color:purple;
 }
</style>


<template>
    <div>
        <h1>hello {{ batchno }}</h1>
    </div>
<!-- 
<input type="number" v-model="num1">
<input type="number" v-model="num2"> -->

<input type="number" v-model="obj.num1">
<input type="number" v-model="obj.num2">
{{ answer2 }}  
<br/>
<h4 v-if="answer2 > 10">More than 10</h4>


</template>




<script setup>
import { computed } from '@vue/reactivity';
import { reactive, ref } from 'vue';


const batchno = ref(40)
let num1 = ref(0)
let num2 = ref(1)

const answer = computed(() => {
    return (num1.value + num2.value)
})

const obj = reactive(
    {
        num1: 0, 
        num2: 0
    })

    
const answer2= computed(() => {
    return (obj.num1 + obj.num2)
})

setInterval(() => {
    batchno.value ++
}, 1000);

</script>