<template>
  <input type="text" v-model="value" />
</template>

<script>
import Cleave from 'cleave.js'

export default {
  props: {
    options: {
      type: Object,
      default: () => ({})
    }
  },

  data () {
    return {
      value: '',
      cleave: null
    }
  },

  mounted () {
    this.cleave = new Cleave(this.$el, this.options)
  },

  beforeDestroy () {
    this.cleave.destroy()
  }

}
</script>
