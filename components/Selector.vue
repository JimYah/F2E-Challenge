<template lang="pug">
  .selector__wrap
    .selector__icon
      i(class="fas fa-caret-down")
    select.selector(
      @change="changeFunction(zone)"
      v-model="zone"
    )
      option(value="所有地區", selected) 所有地區
      option(v-for="option in options", :key="option", :value="option", v-text="option")

</template>

<script>
  export default {
    name: 'Selector',
    props: {
      options: {
        type: Array,
        required: false
      },
      changeFunction: {
        type: Function,
        required: false
      }
    },
    data() {
      return {
        zone: '所有地區'
      }
    }
  }
</script>

<style lang="sass" scoped>
*, *:focus
  box-sizing: border-box
  outline: none

.selector__wrap
  position: relative
  width: 100%
  .selector__icon
    position: absolute
    top: 50%
    right: 20px
    transform: translateY(-50%)
    cursor: pointer
    pointer-event: none
  .selector
    display: block
    width: 100%
    height: 40px
    padding: 0 20px
    background-color: #FFF
    appearance: none
    border: none
    border-radius: 0
    cursor: pointer
    font-size: 16px
</style>