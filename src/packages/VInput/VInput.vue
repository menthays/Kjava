<template lang="html">
  <div class="input-container">
    <input class="input-item"
      :type="type" :name="name"
      :value="currentValue" :placeholder="placeholder"
      @input="changeHandler"
      @focus="focusHandler"
      @blur="blurHandler">
    <transition name="fade">
      <div class="input-msg" v-if="errState">{{errMsg}}</div>
    </transition>

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
  validators: {
    isNonEmpty (value) {
      return value === '' ?
        1 : 0
    },
    minLength (value, length) {
      return value.length < length ?
        1 : 0
    },
    isEmail (value) {
      return !/^\w+([+-.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/.test(value) ?
        1 : 0
    },
    isNumber (value) {
      return !/^[0-9\+]*$/.test(value) ?
        1 : 0
    },
    agreeWith (value, payload) {
      return value === payload ?
        0 : 1
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
      this.$emit('focus', event);
      this.errState = false
    },
    blurHandler (event) {
      this.$emit('blur', event);
      let vm = this;
      let value = event.target.value;
      let validators = vm.$options.validators;
      vm.rules.map((item)=>{
        try {
          if(typeof item.validate === 'function'){
            vm.errState = item.validate(value, item.payload)
          }
          else if(typeof item.validate === 'string'){
            let validator = validators[item.validate]
            vm.errState = validator.call(value, item.payload)
          }
          else{
            throw "Param 'validators' must be function or string!"
          }

          if(vm.errState){
            vm.errMsg = item.errMsg
          }
        } catch (e) {
          console.log("%c"+"[VForm Error] "+e, "color:red;");
        }


      })
    }
  }
}
</script>

<style lang="css">
.input-container {
  /*width: auto;*/
  position: relative;
  height: auto;
}
.input-item {
  width: 100%;
  height: 36px;
  padding: 5px 12px;
  font-size: 18px;
  border: 2px solid #99A9BF;
  border-radius: 3px;
  transition: border-color .3s ease-in-out;
  box-sizing: border-box;
}
.input-item:focus {
  outline: none;
  border-color: #1F2D3D;
}
.input-msg {
  color: #FF4949;
  margin-top: 6px;
  padding-left: 14px;
  width: 100%;
  font-size: 14px;
}
.fade-enter-active {
  transition: opacity .3s
}
.fade-leave-active {
  transition: opacity 0
}
.fade-enter, .fade-leave-to {
  opacity: 0
}
</style>
