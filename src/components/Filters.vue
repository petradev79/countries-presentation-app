<template>
  <div class="filters">
    <div class="filters__search">
      <i class="fas fa-search"></i>
      <input
        @input="$emit('update:modelValue', $event.target.value)"
        type="text"
        placeholder="Search for a country..."
      />
    </div>
    <div class="dropdown">
      <div class="filters__select" @click="isFilterOpen = !isFilterOpen">
        <span>Filter by Region </span> <i class="fas fa-chevron-down"></i>
      </div>
      <div v-show="isFilterOpen" class="dropdown__menu">
        <a
          class="dropdown__link"
          v-for="region in regions"
          :key="region"
          @click="getRegion(region)"
          >{{ region }}</a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFilterOpen: false,
      regions: ['Africa', 'Americas', 'Asia', 'Europe', 'Oceania'],
    };
  },
  methods: {
    getRegion(region) {
      this.$emit('clicked', region);
    },
  },
};
</script>

<style lang="scss" scoped>
.filters {
  padding-block: 2rem;

  @include respond(tab) {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__search {
    position: relative;
    display: flex;
    align-items: center;

    i {
      position: absolute;
      left: 3rem;
      font-size: 1.6rem;
    }

    input {
      width: 100%;
      padding-block: 2rem;
      padding-left: 7rem;
      background: $color-white;
      outline: none;
      border: none;
      border-radius: 0.5rem;
      box-shadow: -1px 1px 2px 1px rgba($color-black, 0.1);
      cursor: pointer;

      @include respond(tab) {
        width: 40rem;
      }

      @include respond(lap) {
        width: 50rem;
      }

      &::placeholder {
        font-size: 1.4rem;
        font-family: inherit;
        color: lighten($color-gray-dark, 10%);
      }
    }
  }

  &__select {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 2rem;
    font-weight: 600;
    background: $color-white;
    border-radius: 0.5rem;
    box-shadow: -1px 1px 2px 1px rgba($color-black, 0.1);
  }
}

.dropdown {
  position: relative;
  width: 60%;
  margin-block: 3rem;
  cursor: pointer;

  @include respond(tab) {
    width: 20rem;
  }

  &__menu {
    position: absolute;
    margin-top: 0.5rem;
    width: 100%;
    padding: 2rem;
    background: $color-white;
    border-radius: 0.5rem;
    box-shadow: -1px 1px 2px 1px rgba($color-black, 0.1);
  }

  &__link {
    display: block;
    text-decoration: none;
    font-weight: 600;

    &:not(:last-child) {
      margin-bottom: 0.5rem;
    }
  }
}
</style>
