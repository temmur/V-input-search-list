<template lang="">
    <div>
        <div>
      <CInput type="text" placeholder="Enter a key word" v-model="search" @on-focus="show = true" />
    </div>
    <div v-if="show && search.length > 2">
      <ul class="filterList list-none rounded-lg border-1 border-white/20 bg-white/10 backdrop-blur-xl pl-4 mt-3">
        <li v-for="(country, index) in filterArr" :key="index"
          class="p-4 pl-0 border-b border-b-white/[0.08] last:border-none"
          
        >
          <p v-if="country.includes(search) === true" v-html="displayResult(country)"></p>
          <p v-if="country.includes(search) === false" ></p>

        </li>
      </ul>
    </div>

    </div>
</template>
<script setup lang="ts">
import CInput from './Form/CInput.vue'
import { countries } from '../constants/countrySlide';
import { onMounted, ref } from 'vue'
const search = ref('')
const show = ref(false)
const item = ref('')
const filterArr = []

function filterArray(){
    const inputValue = search.value.toLowerCase()
    const filterData = countries.filter((item)=>{
        // console.log(item.country.toLowerCase().includes(inputValue));
           filterArr.push(item.country.toLowerCase())
        console.log(typeof filterArr);
    })
}
function displayResult(text){
    if (search.value === '') {
      return text; // Return the original text if search input is empty
    }
    const regex = new RegExp(search.value, 'gi');
    return text.replace(regex, '<mark class="highlight">$&</mark>');
}
onMounted(() => {
    filterArray()
})


</script>
<style scoped>
    
</style>