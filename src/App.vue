<template>
  <div id="app">
    <Header :itens="itensCarrinho" />

    {{ nome }}

    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Header from "./components/Header.vue";

export default {
  name: "App",
  data() {
    return {
      itensCarrinho: {},
      nome: "",
      descricao: "",
      valor: 0,
      desconto: 0,
      estoque: 0,
      fotos: {},
    };
  },
  methods: {
    async getProduto() {
      await fetch("http://localhost:3000/produtos/1")
        .then((r) => r.json())
        .then((r) => {
          this.nome = r.nome;
          this.descricao = r.descricao;
          this.valor = r.valor;
          this.desconto = r.desconto;
          this.estoque = r.estoque;
          this.fotos = r.fotos;
        });
    },
  },
  created() {
    this.getProduto();
  },
  components: {
    HelloWorld,
    Header,
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Kumbh Sans", sans-serif;
  max-width: 1100px;
  margin: 0 auto;
}
</style>
