<template>
    <div class="bg-blue-700 rounded-md p-5 lg:p-10">
        <h2 class="text-white text-3xl font-black block lg:inline-block mr-10 mb-5">Países</h2>
        <div class="bg-white block w-10/12 lg:w-auto lg:inline-block px-5 py-2 rounded-full mx-auto">
            <input
                v-model="search"
                class="w-full bg-transparent outline-none"
                type="text"
                placeholder="Pesquisar..."
            />
        </div>
        <div class="flex flex-wrap justify-between">
            <character-card v-for="character in characters" :key="character" :character="character"></character-card>
        </div>
        <div v-if="characters.length <= 0" class="mt-10 text-center">
            <p class="text-white">Paises não encontrado</p>
        </div>
    </div>
</template>

<script setup>
import CharacterCard from './CharacterCard.vue'
</script>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            characters: [],
            search: ""
        }
    },
    watch: {
        search() {
            this.findCharacter()
        }
    },
    methods: {
        async getAllCharacters() {
            const resp = await axios.get("https://restcountries.eu/rest/v2/all")
            return resp.data
        },
        async findAllCharacters() {
            const data = await this.getAllCharacters()
            this.characters = data.sort((a, b) => {
                if (a.name.trim() > b.name.trim()) return 1
                if (a.name.trim() < b.name.trim()) return -1
                return 0
            })
        },
        async findCharacter() {
            const characters = await this.getAllCharacters()
            if (this.search.length > 0) {
                this.characters = characters.filter((el) => {
                    return el.name.toUpperCase().includes(this.search.toUpperCase())
                })
            } else this.findAllCharacters()
        }
    },
    mounted() {
        this.findAllCharacters()
    }
}
</script>