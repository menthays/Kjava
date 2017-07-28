<template>
  <div class="radio-group">
    <slot></slot>
  </div>
</template>
<script>
  export default {
    name: 'v-radio-group',
    componentName: 'v-radio-group',
    props: {
      value: '',
    },
    watch: {
      value(value) {
        this.$emit('change', value);
      }
    }
  };
</script>
<style lang="stylus">
  .radio-group
    display flex
    justify-content space-around
    align-items center
</style>
