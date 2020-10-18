<template>
  <div id="app">
    <Nav />
    <Clock />
  </div>
</template>

<script>
import Nav from './components/Nav.vue';
import Clock from './components/Clock.vue';

export default {
  name: 'App',
  components: {
    Nav,
    Clock,
  }
}
</script>
