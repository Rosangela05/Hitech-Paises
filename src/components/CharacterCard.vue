<template>
    <div class="bg-white p-7 rounded-md m-5 w-56 flex-auto">
        <img
            :src="character.flag"
            alt="Character's image"
            class="border-gray-500 border-solid border-2 w-20 h-20 rounded-full"
        />
        <p class="text-md text-gray-400 mt-2">#{{ character.name }}</p>
        <p class="bold text-lg">{{ character.capital }}</p>
        <p
            :class="[
                { 'bg-green-500': character.region.includes('Americas') },
                { 'bg-red-500': character.region.includes('Asia') },
                { 'bg-gray-800': character.region.includes('Europe') },
                { 'bg-yellow-500': character.region.includes('Africa') },
                { 'bg-blue-500': character.region.includes('Oceania') },
                 { 'bg-indigo-300': character.region.includes('Polar') },
       
                'bg-gray-300 text-sm inline-block rounded-full px-3 py-1 text-white'
            ]"
        >{{ character.region }}</p>
        <p class="text-gray-700 text-sm mt-2">População: {{ character.population }}</p>

        
    </div>
</template>

<script setup>
import { defineProps } from "vue"
defineProps(["character"])
</script>