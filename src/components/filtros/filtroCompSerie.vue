<script>
import axios from "axios";
import FiltrosApi from "@/api/filtros.js";
const filtrosapi = new FiltrosApi();

export default {
  data() {
    return {
      params: {
        serie: "",
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
      "https://api.themoviedb.org/3/genre/tv/list?api_key=4f2d6721f9937522fb8b76dbac0eab07&language=pt-BR"
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
            <label placeholder="Buscar por serie ou pessoa" for=""></label>
            <input v-model="params.serie" type="text" placeholder="Pesquisar Serie" />
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

<style>

form {
  display: flex;
}
.filmes-filtros {
  display: flex;
  padding: 25px;
  align-items: center;
  justify-content: space-around;
}
.tudo {
  display: flex;
  align-items: center;
}
label {
  font-size: 1.1em;
  font-weight: bold;
  margin-bottom: 5px;
  width: 220px;
}
.sel-filtros {
  display: flex;
  margin: 5px;
  flex-direction: column;
}
.filtro {
  padding: 25px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
}
.button-fil {
  border-radius: 15px;
  height: 45px;
  width: 100px;
  margin-top: 10px;
  background-color: white;
  border: 3px solid rgb(29, 202, 214);
}

.filtro {
  display: flex;
}
.olla{
  margin-top: 40px;
}
.todofiltro {
  margin-left: 32px;
  display: flex;
}
</style>
