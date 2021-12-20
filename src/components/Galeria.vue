<template>
  <div class="galeria">
    <a @click="exibe" href="" class="principal"
      ><img :src="require(`@/assets/${fotos.imagem[0]}`)"
    /></a>

    <a href="" v-for="foto in fotos.thumb" :key="foto"
      ><img :src="require(`@/assets/${foto}`)"
    /></a>
  </div>
</template>

<script>
export default {
  name: "Galeria",
  props: {
    fotos: Object,
  },
  methods: {
    exibe(e) {
      e.preventDefault();
      console.log(this.fotos);
    },
  },
};
</script>

<style lang="scss" scoped>
.galeria {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 4fr 1fr;
  gap: 30px;

  img {
    border-radius: 15px;
  }

  .principal {
    grid-column: 1/5;
  }
}
</style>
