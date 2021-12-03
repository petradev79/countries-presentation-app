<template>
  <div class="header flex">
    <h1 class="header__title">Where in the world?</h1>
    <div class="header__mode" @click="toggleMode">
      <span v-if="!mode" class="header__mode--light"
        ><i class="fas fa-moon"></i> Dark Mode</span
      >
      <span v-else class="header__mode--dark"
        ><i class="far fa-moon"></i> Light Mode</span
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    mode: {
      type: Boolean,
      defoult: false,
    },
  },
  methods: {
    toggleMode() {
      this.$emit('clicked');
    },
  },
};
</script>

<style lang="scss" scoped>
.header {
  position: fixed;
  top: 0;
  width: 100%;
  justify-content: space-between;
  align-items: center;
  padding: 2.5rem 1.5rem;
  background: $color-white;
  box-shadow: 0 4px 2px -2px rgba($color-black, 0.1);
  z-index: 1000;

  @include respond(lap) {
    padding-inline: calc((100% - 128rem) / 2);
  }

  &__title {
    font-size: 1.6rem;
    color: $color-very-dark-text;

    @include respond(lap) {
      font-size: 2rem;
    }
  }

  &__mode {
    font-weight: 800;
    font-size: 1.2rem;
    cursor: pointer;

    @include respond(lap) {
      font-size: 1.6rem;
    }
  }
}
</style>
