<template>
  <header class="flex">
    <div class="flex">
      <a href="#"><img src="../assets/logo.svg" alt="Logo Sneakers" /></a>
      <nav>
        <ul class="flex">
          <li><a href="#">Collections</a></li>
          <li><a href="#">Men</a></li>
          <li><a href="#">Women</a></li>
          <li><a href="#">About</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </nav>
    </div>
    <div class="info flex">
      <a
        href="#"
        v-on:mouseenter="exibeCarrinho"
        v-on:mouseleave="ocultaCarrinho"
        class="cart-icon"
      >
        <span class="qtde-carrinho" v-if="qtdeCarrinho > 0">{{
          qtdeCarrinho
        }}</span>
        <img src="../assets/icon-cart.svg" alt="Cart" />
        <transition appear>
          <div v-show="carrinhoAtivo" class="cart">
            <span>Cart</span>
            <div v-if="itens.length" class="item">
              <ul>
                <li v-for="(item, key) in cartItens" :key="key">
                  <img src="../assets/thumb-1.jpg" alt="" />
                  <span>
                    <p>{{ item.nome }}</p>
                    <p>
                      {{ item.valor }} x{{ item.quantidade }}
                      <strong>{{ item.valorTotal }}</strong>
                    </p>
                  </span>
                  <img
                    @click="removeCarrinho(key)"
                    src="../assets/icon-delete.svg"
                    alt=""
                  />
                </li>
              </ul>
              <button>Checkout</button>
            </div>
            <div v-else class="empty">
              <p>Your cart is empty.</p>
            </div>
          </div>
        </transition>
      </a>
      <a href="#" class="avatar"
        ><img src="../assets/image-avatar.png" alt="User"
      /></a>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    itens: Array,
  },
  data() {
    return {
      carrinhoAtivo: false,
      cartItens: this.itens,
    };
  },
  methods: {
    removeCarrinho(index) {
      this.cartItens.splice(index, 1);
    },
    exibeCarrinho() {
      this.carrinhoAtivo = true;
    },
    ocultaCarrinho() {
      this.carrinhoAtivo = false;
    },
  },
  computed: {
    qtdeCarrinho() {
      return this.cartItens.reduce((acc, item) => {
        return acc + item.quantidade;
      }, 0);
    },
  },
};
</script>

<style lang="scss" scoped>
.flex {
  display: flex;
  align-items: center;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s;
}
.v-enter,
.v-leave-to {
  opacity: 0;
}

header {
  justify-content: space-between;
  padding: 30px 0;
  border-bottom: 1px solid hsl(220, 14%, 90%);
  position: relative;
}

nav ul {
  margin-left: 40px;

  a {
    color: hsl(219, 9%, 45%);
    margin-left: 15px;
    padding: 10px;
    transition: color 0.3s, box-shadow 0.3s;

    &:hover {
      color: hsl(220, 13%, 13%);
      box-shadow: 0px 29px 0px #ffffff, 0px 32px 0px hsl(26, 100%, 55%);
    }
  }
}

.avatar {
  max-width: 45px;
  margin-left: 40px;
  transition: 0.3s;

  &:hover {
    color: hsl(220, 13%, 13%);
    border-radius: 50%;
    box-shadow: 0px 0px 0px 2px hsl(26, 100%, 55%);
  }
}

.cart-icon {
  position: relative;

  .qtde-carrinho {
    position: absolute;
    top: -5px;
    right: -5px;
    font-size: 10px;
    font-weight: 700;
    padding: 0px 6px;
    border-radius: 40%;
    color: #fff;
    background: hsl(26, 100%, 55%);
  }
}

.cart {
  border-radius: 5px;
  background-color: white;
  box-shadow: -5px 5px 100px -30px rgba(0, 0, 0, 0.25);
  width: 360px;
  position: absolute;
  right: 0px;
  top: 0px;
  margin-top: 20px;
  left: 50%;
  transform: translateX(-50%);
  cursor: default;

  .empty {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    min-height: 150px;

    p {
      text-align: center;
      font-weight: 700;
      color: hsl(219, 9%, 45%);
    }
  }

  .item {
    padding: 25px;
    color: hsl(219, 9%, 45%);

    li {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 20px;

      & img:first-child {
        max-width: 50px;
        border-radius: 8px;
      }

      & img:last-child {
        cursor: pointer;
      }
    }

    span {
      margin: 0px 15px;

      & p:first-child {
        margin-bottom: 5px;
      }

      strong {
        font-weight: 700;
        color: hsl(0, 0%, 0%);
      }
    }

    button {
      font-family: "Kumbh Sans", sans-serif;
      font-size: 16px;
      border-radius: 8px;
      border: none;
      background: hsl(26, 100%, 55%);
      color: #fff;
      font-weight: 700;
      padding: 16px 0;
      cursor: pointer;
      width: 100%;
    }
  }

  & > span {
    display: block;
    color: hsl(0, 0%, 0%);
    border-bottom: 1px solid hsl(220, 14%, 90%);
    padding: 20px;
    font-weight: 700;
  }
}
</style>
