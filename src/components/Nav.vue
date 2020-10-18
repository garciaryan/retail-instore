<template>
  <header>
    <ul class="nav">
      <li
        class="city"
        v-for="(city, index) in cities"
        :key="index"
        :class="{ 'is-active': city.section === activeCity }">
        <a @click="activate(city.section)"
          href="#">
          {{ city.label }}
        </a>
      </li>
    </ul>
    <div class="line"></div>
  </header>
</template>

<style lang="scss">
  @import '../scss/Nav.scss';
</style>

<script>
  import { cities } from '../../navigation.json';
  import axios from 'axios';

  // Usually I'd put this in a .env file or somewhere secure!
  const API_KEY = 'AIzaSyAEfLS3E7ui8Ek5YhteeI7HAYtiy0WrKcY';

  export default {
    data() {
      return {
        cities,
        activeCity: 'cupertino',
        coords: {
          'cupertino': '37.3229978,-122.0321823',
          'new-york-city': '40.7142691,-74.0059729',
          'london': '51.5074,0.1278',
          'amsterdam': '52.3676,4.9041',
          'tokyo': '35.6762,139.6503',
          'hong-kong': '22.3193,114.1694',
          'sydney': '-33.8688,151.2093'
        },
      }
    },

    mounted() {
      this.getTime(this.activeCity);
    },

    methods: {
      activate(city) {
        this.activeCity = city;
        this.getTime(city);
      },

      getTime(city) {
        let seconds = new Date().getTime() / 1000;
        const URL = `https://maps.googleapis.com/maps/api/timezone/json?location=${this.coords[city]}&timestamp=${seconds}&key=${API_KEY}`

        axios.get(URL)
          .then(res => {
            let { dstOffset, rawOffset } = res.data;
            let localDate = new Date((seconds + dstOffset + rawOffset) * 1000);
            this.$root.$emit('time', localDate)
          })
          .catch(err => {
            console.error(err);
          })
      }
    }
  }
</script>