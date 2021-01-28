<template>
  <v-app>
    <Header />
    <template class="d-flex">
      <v-navigation-drawer app clipped color="#B22222" dark>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title"> Gerações </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-spacer />
        <v-list-item-group>
          <v-list nav v-for="(item, index) in 8" :key="index">
            <v-list-item link @click="generation(index + 1)">
              Geração {{ index + 1 }}
            </v-list-item>
          </v-list>
        </v-list-item-group>
      </v-navigation-drawer>
      <v-main style="backgroundcolor: #f1f1f1">
        <div v-if="status !== 200" class="d-flex justify-space-around pa-10">
          <v-progress-circular
            :size="70"
            :width="7"
            color="red"
            indeterminate
          ></v-progress-circular>
        </div>
        <div v-else class="pa-10">
          <div class="d-flex">
            <v-text-field
              v-model="busca"
              outlined
              label="Pesquisar"
              filled
              rounded
              dense
            >
            </v-text-field>

            <v-btn icon color="black" class="ml-2 mr-2" @click="search">
              <v-icon>mdi-magnify</v-icon>
            </v-btn>
            <v-btn icon color="black" @click="clean">
              <v-icon>mdi-delete </v-icon>
            </v-btn>
          </div>
          <div class="d-flex flex-wrap justify-space-around">
            <HelloWorld
              v-for="poke in filteredPokemons"
              :key="poke.url"
              :name="poke.name"
              :url="poke.url"
            />
          </div>
        </div>
      </v-main>
    </template>
  </v-app>
</template>

<script>
import Header from "./components/Header";
import HelloWorld from "./components/HelloWorld";
import axios from "axios";

export default {
  name: "App",

  components: {
    Header,
    HelloWorld,
  },

  data: () => ({
    pokemons: [],
    filteredPokemons: [],
    busca: "",
    status: 0,
  }),

  methods: {
    search: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name.indexOf(this.busca) > -1
        );
      }
    },
    clean: function () {
      this.busca = "";
      this.filteredPokemons = this.pokemons;
    },
    generation: function (index) {
      switch (index) {
        case 1:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        case 2:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=100&offset=151")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        case 3:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=135&offset=251")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        case 4:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=107&offset=386")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        case 5:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=156&offset=493")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        case 6:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=72&offset=649")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        case 7:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=88&offset=721")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        case 8:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=89&offset=809")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
        default:
          axios
            .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
            .then((res) => {
              this.pokemons = res.data.results;
              this.filteredPokemons = res.data.results;
            });
          this.load();
          break;
      }
    },

    load: function () {
      setTimeout(() => {
        this.status = 200;
      }, 2000);
      this.status = 0;
    },
  },

  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
    this.load();
  },
};
</script>

