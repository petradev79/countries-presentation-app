<template>
  <div class="details container">
    <Button @click="$router.push('/')" />
    <div class="country">
      <div class="country__img">
        <img :src="country.flag" :alt="country.name" />
      </div>
      <div class="country__details">
        <h2 class="country__title">{{ country.name }}</h2>
        <div class="country__cta">
          <div class="country__cta--top">
            <p>
              Native Name: <span>{{ country.nativeName }}</span>
            </p>
            <p>
              Population: <span>{{ country.population }}</span>
            </p>
            <p>
              Region: <span>{{ country.region }}</span>
            </p>
            <p>
              Sub Region: <span>{{ country.subregion }}</span>
            </p>
            <p>
              Capital: <span>{{ country.capital }}</span>
            </p>
          </div>
          <div class="country__cta--bottom">
            <p>
              Top Level Domain:
              <span v-for="(top, i) in country.topLevelDomain" :key="i">{{
                top
              }}</span>
            </p>
            <p>
              Currencies:
              <span v-if="country.currencies"
                >{{ generateArr(country.currencies) }}
              </span>
            </p>
            <p>
              Languages:
              <span v-if="country.languages"
                >{{ generateArr(country.languages) }}
              </span>
            </p>
          </div>
        </div>
        <div class="country__borders" v-if="country.borders">
          <p>Border Countries:</p>
          <div class="country__borders-box flex">
            <span
              v-for="(border, i) in generateBorders(country.borders)"
              :key="i"
              @click="borderCountry(border)"
              >{{ border.name }}</span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { BASE_URL } from '@/config';
import Button from '@/components/Button.vue';

export default {
  components: { Button },
  data() {
    return {
      name: this.$route.params.name,
      country: {},
      countries: [],
    };
  },
  created() {
    this.getCountry(`${BASE_URL}/name/${this.name}`);
    this.countries = JSON.parse(localStorage.getItem('countries'));
  },
  methods: {
    borderCountry(border) {
      this.getCountry(`${BASE_URL}/name/${border.name}`);
    },
    async getCountry(url) {
      try {
        const res = await fetch(url);
        if (!res.ok) throw Error('Sorry, this content is unavailable');
        const data = await res.json();
        this.country = data[0];
      } catch (err) {
        this.errMsg = err.message;
      }
    },
    generateArr(arr) {
      return arr.map(item => item.name).join(', ');
    },
    generateBorders(arr) {
      const borders = this.countries.filter(country => {
        return arr.some(code => {
          return country.alpha3Code === code;
        });
      });
      return borders;
    },
  },
};
</script>

<style lang="scss" scoped>
.country {
  @include respond(lap) {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__img {
    @include respond(lap) {
      width: 45%;
    }
  }

  &__details {
    margin-top: 3rem;

    @include respond(lap) {
      width: 45%;
    }

    span {
      font-weight: 400;
    }
  }
  &__title {
    margin-bottom: 2rem;
    font-size: 2.4rem;
    font-weight: 800;
    color: $color-very-dark-text;

    @include respond(lap) {
      margin-bottom: 3rem;
      font-size: 2.8rem;
      letter-spacing: 1px;
    }
  }
  &__cta {
    font-weight: 600;
    margin-bottom: 3rem;

    @include respond(tab) {
      display: flex;
      justify-content: space-between;
      align-items: top;
    }

    @include respond(lap) {
      font-size: 1.6rem;
    }

    &--top {
      margin-bottom: 3rem;

      @include respond(lap) {
        margin-bottom: 0;
      }

      p {
        margin-bottom: 1rem;
      }
    }

    &--bottom {
      p:not(:last-child) {
        margin-bottom: 1rem;
      }
    }
  }
  &__borders {
    p {
      margin-bottom: 1rem;
      font-size: 1.6rem;
      font-weight: 600;

      @include respond(lap) {
        margin-bottom: 2rem;
        font-size: 1.8rem;
      }
    }
    span {
      padding: 0.5rem 2rem;
      font-size: 1.2rem;
      border-radius: 0.5rem;
      box-shadow: -1px 1px 2px 1px rgba($color-black, 0.1);
      font-size: 1.4rem;
      cursor: pointer;
    }
  }
  &__borders-box {
    flex-wrap: wrap;
    --gap-space: 0.7rem;
  }
}
</style>
