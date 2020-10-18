<template>
  <div class="clock">
    <h1>{{ time }}</h1>
  </div>
</template>

<style lang="scss">
  @import '../scss/Clock.scss';
</style>

<script>
export default {
  data() {
    return {
      time: ''
    }
  },

  mounted() {
    this.$root.$on('time', data => {
      this.time = data;
    })
  },
}
</script>