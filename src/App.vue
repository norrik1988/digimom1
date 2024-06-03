<script setup>
import Dashboard from './components/Dashboard.vue'

</script>

<template>
<div class="background">
  <Dashboard></Dashboard>
</div>
</template>

<style>
@import url('../node_modules/primeflex/primeflex.css');

.background {
  background-image: url(./public/beautiful-mountains-landscape.jpg);
  background-size: cover;
  background-position: center;
  padding: 20px;
}

</style>
