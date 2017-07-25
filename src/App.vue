<template>
  <div id="app">
    <h1>Input</h1>
    <v-input class="input" :rules="ruleA" v-model="msg" type="password"></v-input>
  </div>
</template>

<script>
import VInput from './packages/VInput/VInput.vue'
export default {
  name: 'app',
  data () {
    return {
      msg: 'test',
      ruleA: [
        {
          validate: this.fn,
          errMsg: 'must be number',
          payload: null
        }
      ]
    }
  },
  components: {
    'v-input': VInput
  },
  methods: {
    fn (value, payload) {
      return !/^[0-9\+]*$/.test(value) ?
         1 : 0
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.input {
  width: 200px;
}
</style>
