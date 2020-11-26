<template>
<div id="app">
    <img src="./assets/logo.png" alt="" />

    <div class="column is-half is-offset-one-quarter">
        <hr />

        <h4 class="is-size-4">POKEDEX</h4>
        <input type="text" placeholder="Buscar Pokemon" v-model="busca" class="input is-rounded" />
        <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">
            Buscar
        </button>
        <div v-for="(poke, index) in filteredPokemons" :key="poke.name">
            <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
        </div>
    </div>
</div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
    name: "App",
    data() {
        return {
            pokemons: [],
            busca: "",
            filteredPokemons: [],
        };
    },
    created: function () {
        axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
            .then((res) => {
                this.pokemons = res.data.results;
                this.filteredPokemons = res.data.results;
            });
    },
    components: {
        Pokemon,
    },
    methods: {
        buscar: function () {
            if (this.busca == "" || this.busca == " ") {
                this.filteredPokemons = this.pokemons;
            } else {
                this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
            }

        }
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

#buscaBtn {
    margin-top: 1%;
    margin-bottom: 2%;
}
</style>
