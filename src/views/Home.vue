<template>
  <div class="home container">
    <Filters @clicked="onGetRegion" v-model="searchValue" />
    <div class="message" v-if="errMsg">{{ errMsg }}</div>
    <Countries :countries="searchResult" />
  </div>
</template>

<script>
import { BASE_URL } from '@/config';
import Countries from '@/components/Countries.vue';
import Filters from '@/components/Filters.vue';

export default {
  name: 'Home',
  components: { Countries, Filters },
  data() {
    return {
      errMsg: '',
      countries: [],
      searchValue: '',
    };
  },
  mounted() {
    this.getData(`${BASE_URL}all`);
  },
  computed: {
    searchResult() {
      if (this.searchValue) {
        return this.countries.filter(country => {
          return this.searchValue
            .toLowerCase()
            .split(' ')
            .every(v => country.name.toLowerCase().includes(v));
        });
      } else {
        return this.countries;
      }
    },
  },
  methods: {
    onGetRegion(region) {
      this.getData(`${BASE_URL}region/${region}`);
    },
    async getData(url) {
      try {
        const res = await fetch(url);
        if (!res.ok) throw Error('Sorry, this content is unavailable');
        const data = await res.json();
        this.countries = data.map(this.generateCountry);
        localStorage.setItem('countries', JSON.stringify(this.countries));
      } catch (err) {
        this.errMsg = err.message;
      }
    },
    generateCountry(country) {
      const { flag, name, population, region, capital, alpha3Code } = country;

      return { flag, name, population, region, capital, alpha3Code };
    },
  },
};
</script>

<style lang="scss" scoped>
.message {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  font-size: 5rem;
  font-weight: 800;
  color: $color-gray-dark;
}
</style>
