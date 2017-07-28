<template>
  <div id="app">
    <h1>Input</h1>
    <v-input class="input" :rules="ruleA" v-model="msg" type="text"></v-input>
    <h1>Accordion</h1>
    <v-rg v-model="radioValue">
      <v-rb label="3"></v-rb>
      <v-rb label="6"></v-rb>
    </v-rg>
  </div>
</template>

<script>
import VInput from './packages/VInput'
import rg from './packages/VRadio/radio_group.vue'
import rb from './packages/VRadio/radio_button.vue'
export default {
  name: 'app',
  data () {
    return {
      msg: 'test',
      ruleA: [
        {
          validate: 'isEmail',
          errMsg: 'Must be Email!',
          payload: null
        }
      ],
      radioValue: '3'
    }
  },
  components: {
    'v-input': VInput, 'v-rg': rg, 'v-rb': rb
  },
  methods: {

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
.a{
  box-sizing: border-box;
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
