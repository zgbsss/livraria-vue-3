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
    editar(autor) {
      Object.assign(this.autores, autor);
    },
    async excluir(autor) {
      await autoresApi.excluirAutor(autor.id);
      this.autores = await autoresApi.buscarTodosOsAutores();
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
    <span @click="editar(autor)">{{ autor.id }} {{ autor.nome }}</span>
    <button @click="excluir(autor)">X</button>
  </li>
</template>
