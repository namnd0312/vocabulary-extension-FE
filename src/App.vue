<template>
  <div id="app" class="h-100">
    <div class="container-fluid h-100">
      <div class="row h-100">
        <div class="col-md-12 h-100 d-flex justify-content-center align-items-center">
          <div class="col-md-6 rounded px-5 py-4 shadow bg-white text-left">
            <Vocabulary />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vocabulary from './components/Vocabulary.vue'

export default {
  name: 'App',
  components: {
    Vocabulary
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.vue-bg {
  background: #bce5d0;
}
</style>
