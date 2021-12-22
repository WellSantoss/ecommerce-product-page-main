<template>
  <div class="galeria">
    <div class="principal">
      <img
        v-if="imagemPrincipal"
        :src="require(`@/assets/${imagemPrincipal}`)"
      />
    </div>

    <div
      v-for="(thumb, i) in thumbs"
      :class="{ active: thumbAtivo == i }"
      :key="i"
      @click="changePrincipal(i)"
    >
      <img :src="require(`@/assets/${thumb}`)" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Galeria",
  props: {
    fotos: Object,
  },
  data() {
    return {
      imagemPrincipal: null,
      thumbAtivo: 0,
      imagens: [],
      thumbs: [],
    };
  },
  methods: {
    changePrincipal(index) {
      this.imagemPrincipal = this.imagens[index];
      this.thumbAtivo = index;
    },
  },
  watch: {
    fotos() {
      this.imagemPrincipal = this.fotos.imagem[0];
      this.imagens = this.fotos.imagem;
      this.thumbs = this.fotos.thumb;
    },
  },
  computed: {},
};
</script>

<style lang="scss" scoped>
.galeria {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 5fr 1fr;
  gap: 30px;

  div {
    border-radius: 17px;
    cursor: pointer;

    img {
      border-radius: 15px;
    }

    &.principal {
      grid-column: 1/5;
    }

    &.active {
      border: 2px solid hsl(26, 100%, 55%);

      img {
        filter: opacity(40%);
      }
    }
  }
}
</style>
