<template>
  <Header :mode="isDarkMode" @clicked="onToggleMode" />
  <router-view />
</template>

<script>
import Header from '@/components/Header.vue';

export default {
  components: { Header },
  data() {
    return {
      isDarkMode: false,
    };
  },
  methods: {
    onToggleMode() {
      this.isDarkMode = !this.isDarkMode;
      document.body.classList.toggle('dark');
    },
  },
};
</script>

<style lang="scss">
.dark {
  color: $color-white;
  background: $color-very-dark-blue;

  .header,
  .countries .country {
    background: $color-dark-blue;

    &__title {
      color: $color-white;
    }
  }

  .filters .filters__search {
    i {
      color: $color-white;
    }

    input {
      background: $color-dark-blue;
      color: $color-white;
    }
  }

  .filters .dropdown__menu,
  .filters .filters__select {
    background: $color-dark-blue;
    color: $color-white;
  }

  .details {
    .country__title {
      color: $color-white;
    }

    .btn {
      background: $color-dark-blue;
      color: darken($color-white, 30%);
    }

    .country__borders {
      span {
        background: $color-dark-blue;
        color: darken($color-white, 30%);
      }
    }
  }
}
</style>
