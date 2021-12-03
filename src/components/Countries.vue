<template>
  <div class="countries flex" v-if="countries.length">
    <div
      class="country"
      v-for="country in countries"
      :key="country.alpha3Code"
      @click="chooseCountry(country)"
    >
      <img class="country__img" :src="country.flag" :alt="country.name" />
      <div class="country__cta">
        <h2 class="country__title">{{ country.name }}</h2>
        <p><span>Population:</span> {{ country.population }}</p>
        <p><span>Region:</span> {{ country.region }}</p>
        <p><span>Capital:</span> {{ country.capital }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    countries: {
      type: Array,
    },
  },
  methods: {
    chooseCountry(country) {
      this.$router.push({
        name: 'CountryDetails',
        params: { name: country.name },
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.countries {
  flex-wrap: wrap;
  justify-content: center;
  --gap-space: 4rem;

  @include respond(lap) {
    --gap-space: 8rem;
  }
}

.country {
  width: 26rem;
  background: $color-white;
  border-radius: 0.7rem;
  overflow: hidden;
  cursor: pointer;

  &__cta {
    padding: 2rem;

    p {
      margin-bottom: 0.7rem;
    }

    span {
      font-weight: 600;
    }
  }

  &__title {
    margin-bottom: 1.5rem;
    font-size: 1.8rem;
    font-weight: 800;
    color: $color-very-dark-text;
  }
}
</style>
