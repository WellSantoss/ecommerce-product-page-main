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
        ><img src="../assets/icon-cart.svg" alt="Cart" />
        <transition appear>
          <div v-show="carrinhoAtivo" class="cart">
            <span>Cart</span>
            <div>
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
  data() {
    return {
      carrinhoAtivo: false,
    };
  },
  methods: {
    exibeCarrinho(e) {
      this.carrinhoAtivo = true;
    },
    ocultaCarrinho(e) {
      this.carrinhoAtivo = false;
    },
  },
  props: {
    itens: Object,
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
}

.cart {
  border-radius: 5px;
  background-color: white;
  box-shadow: -5px 5px 100px -30px rgba(0, 0, 0, 0.25);
  width: 350px;
  position: absolute;
  right: 0px;
  top: 0px;
  margin-top: 20px;
  left: 50%;
  transform: translateX(-50%);

  & > div {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    min-height: 150px;
  }

  span {
    display: block;
    color: hsl(0, 0%, 0%);
    border-bottom: 1px solid hsl(220, 14%, 90%);
    padding: 20px;
    font-weight: 700;
  }

  p {
    text-align: center;
    font-weight: 700;
    color: hsl(219, 9%, 45%);
  }
}
</style>
