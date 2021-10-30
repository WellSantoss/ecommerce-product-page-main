<template>
  <div id="app">
    <Header :itens="itensCarrinho" />

    <main>
      <div class="container">
        <div class="teste"></div>
        <div class="prod-info">
          <h2>Sneaker Company</h2>
          <h1>{{ nome }}</h1>
          <p>{{ descricao }}</p>
          <div class="flex">
            <h3>
              {{ formtatCurrency(valorDesconto) }}
            </h3>
            <span v-if="desconto > 0" class="desconto">{{
              `${desconto}%`
            }}</span>
          </div>
          <span v-if="desconto > 0" class="valor">{{
            formtatCurrency(valor)
          }}</span>
          <div class="buttons-wrapper flex">
            <div class="quantidade flex">
              <img
                @click="descQuantidade"
                src="./assets/icon-minus.svg"
                alt="Menos"
              />
              <span>{{ quantidade }}</span>
              <img
                @click="ascQuantidade"
                src="./assets/icon-plus.svg"
                alt="Mais"
              />
            </div>
            <button @click="addCarrinho" class="flex">
              <img src="./assets/icon-cart.svg" alt="Carrinho" /><span
                >Add to cart</span
              >
            </button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import Header from "./components/Header.vue";

export default {
  name: "App",
  data() {
    return {
      itensCarrinho: [],
      nome: "",
      descricao: "",
      valor: 0,
      valorDesconto: 0,
      desconto: 0,
      estoque: 0,
      quantidade: 0,
      fotos: {},
    };
  },
  methods: {
    addCarrinho() {
      this.itensCarrinho.push({
        nome: this.nome,
        quantidade: this.quantidade,
        valor: this.formtatCurrency(this.valorDesconto),
        valorTotal: this.formtatCurrency(this.valorDesconto * this.quantidade),
      });

      console.log(this.itensCarrinho);
    },
    ascQuantidade() {
      if (this.quantidade < this.estoque) {
        this.quantidade++;
      }
    },
    descQuantidade() {
      if (this.quantidade > 0) {
        this.quantidade--;
      }
    },
    formtatCurrency(valor) {
      return valor.toLocaleString("en-US", {
        style: "currency",
        currency: "USD",
      });
    },
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

          this.valorDesconto =
            r.desconto > 0 ? r.valor * (r.desconto / 100) : r.valor;
        });
    },
  },
  created() {
    this.getProduto();
  },
  components: {
    Header,
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Kumbh Sans", sans-serif;
  max-width: 1100px;
  margin: 0 auto;
  color: hsl(0, 0%, 0%);
}

.flex {
  display: flex;
  align-items: center;
}

.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: 125px;
  padding: 0 45px;

  .teste {
    min-height: 565px;
    background: tomato;
  }

  .prod-info {
    h2 {
      text-transform: uppercase;
      color: hsl(26, 100%, 55%);
      font-size: 12px;
      font-weight: 700;
      letter-spacing: 2px;
    }

    h1 {
      font-size: 44px;
      font-weight: 700;
      margin: 20px 0 40px;
    }

    p {
      color: hsl(219, 9%, 45%);
      line-height: 24px;
      margin-bottom: 25px;
    }

    h3 {
      font-size: 30px;
      font-weight: 700;
      display: inline-block;
    }

    .desconto {
      color: hsl(26, 100%, 55%);
      background: hsl(25, 100%, 94%);
      padding: 2px 8px;
      border-radius: 5px;
      font-weight: 700;
      margin-left: 15px;
    }

    .valor {
      color: hsl(220, 14%, 75%);
      font-weight: 700;
      text-decoration: line-through;
      display: block;
      margin-top: 8px;
    }

    .buttons-wrapper {
      margin-top: 35px;
    }

    .quantidade {
      border-radius: 8px;
      background: hsl(223, 64%, 98%);
      padding: 10px 5px;
      margin-right: 15px;

      img {
        cursor: pointer;
        padding: 10px;
      }

      span {
        margin: 0 25px;
        font-weight: 700;
        width: 10px;
        text-align: center;
      }
    }

    button {
      font-family: "Kumbh Sans", sans-serif;
      font-size: 16px;
      border-radius: 8px;
      border: none;
      background: hsl(26, 100%, 55%);
      box-shadow: 0 2px 40px -10px hsl(26, 100%, 55%);
      color: #fff;
      font-weight: 700;
      padding: 16px 75px;
      cursor: pointer;

      img {
        margin-right: 15px;
      }
    }
  }
}
</style>
