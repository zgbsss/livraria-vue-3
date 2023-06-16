<script>
import AutoresApi from "../api/autores";
const autoresApi = new AutoresApi();
export default {
  data() {
    return {
      autores: [],
      autor: {},
    };
  },
  async created() {
    this.autores = await autoresApi.buscarTodosOsAutores();
  },
  methods: {
    async salvar() {
      if (this.autor.id) {
        await autoresApi.atualizarAutor(this.autor);
      } else {
        await autoresApi.adicionarAutor(this.autor);
      }
      (this.autor = {}),
        (this.autores = await autoresApi.buscarTodosOsAutores());
    },
  },
};
</script>

<template>
  <h1>Autores</h1>
  <hr />
  <div class="form">
    <input type="text" v-model="autor.nome" placeholder="Nome" />
    <button @click="salvar">Salvar</button>
  </div>
  <hr />
  <li v-for="autor in autores" :key="autor.id">
    <span>{{ autor.id }} {{ autor.nome }}</span>
    <button>X</button>
  </li>
</template>
