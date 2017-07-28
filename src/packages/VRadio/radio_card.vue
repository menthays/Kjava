<template>
  <label
    class="radio-wrapper"
    :class="{'is-active': value === label}"
  >
    <input
      class="radio-input"
      :value="label"
      type="radio"
      v-model="value"
    >
    <div class="radio-block-up">
      <span class="cur">HK$</span>
      <span class="cost">60</span>
      <span class="mon">/mon</span>
    </div>
    <div class="radio-block-down">
      <p>1 CPU</p>
      <p>1GB Memory</p>
    </div>
  </label>
</template>
<script>
  export default {
    name: 'v-radio-card',
    props: ['label'],
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
      flex-direction column
      justify-content space-around
      align-items center
      width 210px
      height 280px
      &:hover
        box-shadow 0 6px 15px rgba(194,194,194,.8)
        border-color rgba(180,180,180,1)
      &.is-active
        box-shadow 0 6px 15px rgba(194,194,194,.8)
        border-color #CB2E35

    &-input
      position absolute
      left -999px
      z-index -999
      cursor pointer
    &-block-up
      width 100%
      height auto
      flex 0 0 auto
      display flex
      justify-content center
      align-items center
      color #A8A8A8
      &>.cur
        align-self flex-start
        padding-right 5px
        // font-size 14px
      &>.cost
        align-self center
        color #000
        font 40px bold
      &>.mon
        padding-left 5px
        align-self flex-end
        // font-size 14px
    &-block-down
      color #A8A8A8
      font-size 18px
      text-align center

</style>
