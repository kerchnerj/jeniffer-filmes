<script>
import axios from "axios";
import FiltrosApi from "@/api/filtros.js";
const filtrosapi = new FiltrosApi();

export default {
  data() {
    return {
      params: {
        filme: "",
        genero: "",
      },
      generos: [],
    };
  },
  methods: {
    buscar() {
      this.$emit("buscar", this.params);
    },
  },
  async created() {
    const { data } = await axios.get(
      "https://api.themoviedb.org/3/genre/movie/list?api_key=df0a1976ab5aa969146a8dbff08f0123&language=pt-BR"
    );
    this.generos = data.genres;
  },
};
</script>
<template>
  <div class="todofiltro">
    <div class="filtro">
      <h3 class="olla">Pesquisar</h3>
      <div class="tudo">
        <form @submit.prevent="buscar">
          <div class="sel-filtros">
            <label placeholder="Buscar por filme ou pessoa" for=""></label>
            <input v-model="params.filme" type="text" placeholder="Pesquisar Filmes" />
          </div>
          <div class="sel-filtros">
            <label for="genre"></label>
            <select v-model="params.genero" id="genre">
              <option disabled value="">Escolha um gênero</option>
              <option
                v-for="genero of generos"
                :key="genero.id"
                :value="genero.id"
              >
                {{ genero.name }}
              </option>
            </select>
          </div>
          <button class="button-fil" type="submit" @click="buscar">
            Buscar
          </button>
        </form>
      </div>
    </div>
  </div>
</template>
