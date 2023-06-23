<script>
import LivrosApi from "../api/livros";
const livrosApi = new LivrosApi();
export default {
  data() {
    return {
      livros: [],
      livro: {},
    };
  },
  async created() {
    this.livros = await livrosApi.buscarTodosOsLivros();
  },
  methods: {
    async salvar() {
      if (this.livro.id) {
        await livrosApi.atualizarLivro(this.livro);
      } else {
        await livrosApi.adicionarLivro(this.livro);
      }
      this.livro = [];
      this.livros = await livrosApi.buscarTodosOsLivros();
    },
  },
};
</script>

<template>
  <h1>Livros</h1>
  <hr />
  <div class="form">
    <input type="text" v-model="livro.titulo" placeholder="Nome" />
    <button @click="salvar">Salvar</button>
  </div>
  <hr />
  <li v-for="livro in livros" :key="livro.id">
    <span> {{ livro.id }} {{ livro.titulo }}</span>
    <button>X</button>
  </li>
</template>
