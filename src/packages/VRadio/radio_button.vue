<template>
  <label
    class="radio-wrapper"
    :class="{'is-active': value === label}"
  >
    <div class="radio-tag-up">
      test
    </div>
    <input
      class="radio-input"
      :value="label"
      type="radio"
      v-model="value"
    >
    <div class="radio-block">
      {{label}} Month
    </div>
    <div class="radio-tag-down">
      test
    </div>
  </label>
</template>
<script>
  export default {
    name: 'v-radio-button',
    props: {
      label: {
        type: String,
        default: '1',
        validate: function (value) {
          return !/^[0-9\+]*$/.test(value) ?
            1 : 0
        }
      }
    },
    data () {
      return {

      }
    },
    computed: {
      value: {
        get() {
          return this._radioGroup.value;
        },
        set(value) {
          this._radioGroup.$emit('input', value);
        }
      },
      _radioGroup() {
        let parent = this.$parent;
        while (parent) {
          if (parent.$options.componentName !== 'v-radio-group') {
            parent = parent.$parent;
          } else {
            return parent;
          }
        }
        return false;
      }
    }
  };
</script>
<style lang="stylus">
  .radio
    &-wrapper
      padding 40px 30px
      border-radius 3px
      border 2px solid rgba(194,194,194,.7)
      box-sizing border-box
      display flex
      position relative
      flex-direction column
      justify-content space-around
      align-items center
      width 180px
      height 120px
      color #A8A8A8
      &:hover
        box-shadow 0 6px 15px rgba(194,194,194,.8)
        border-color rgba(180,180,180,1)
        color #000
      &.is-active
        box-shadow 0 6px 15px rgba(194,194,194,.8)
        border-color #CB2E35
        color #000

    &-input
      position absolute
      left -999px
      z-index -999
      cursor pointer
    &-block
      font-size 32px
    &-tag-up
      position absolute
      top 0
    &-tag-down
      position absolute
      bottom 0
</style>
