<template lang="html">
  <div class="input-container">
    <input class="input-item"
      :type="type" :name="name"
      :value="currentValue" :placeholder="placeholder"
      @input="changeHandler"
      @focus="focusHandler"
      @blur="blurHandler">
    <div class="input-msg" v-if="errState">{{errMsg}}</div>
  </div>
</template>

<script>
export default {
  props: {
    value: String,
    rules: Array,
    type: {
      type: String,
      default: 'text',
      validate: function (value) {
        return (value === 'text' || value === 'password')
      }
    },
    name: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    }
  },
  data () {
    return {
      currentValue: this.value,
      errState: false,
      errMsg: ''
    }
  },
  methods: {
    changeHandler (event) {
      let value = event.target.value;
      this.$emit('input', value);
      this.currentValue = value
      this.$emit('change', value);
    },
    focusHandler () {
      this.errState = false
    },
    blurHandler (event) {
      let vm = this;
      let value = event.target.value;
      vm.rules.map((item)=>{
        if(item.validate(value, item.errMsg, item.payload)){
          vm.errState = true
          vm.errMsg = item.errMsg
        }
      })
    }
  }
}
</script>

<style lang="css">
.input-container{
  /*width: auto;*/
  position: relative;
  height: auto;
  text-align: center;
}
.input-item{
  width: 100%;
  padding: 2px 6px;
  font-size: 18px;
  box-sizing: border-box;
  border: 1px solid #1F2D3D;
  border-radius: 3px;
}
.input-msg {
  color: #FF4949;
  margin-top: 6px;
  width: 100%;
  font-size: 14px;
}
</style>
