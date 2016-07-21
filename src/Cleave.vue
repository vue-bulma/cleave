<template>
  <input type="text" v-mode="value" />
</template>

<script>
import Cleave from './cleave.js'

export default {
  props: {
    value: {
      type: String,
      default: ''
    },
    options: {
      type: Object,
      default: () => ({})
    }
  },

  data () {
    return {
      cleave: null
    }
  },

  ready () {
    this.cleave = new Cleave(this.$el, this.options)
  },

  beforeDestroy () {
    this.cleave.destroy()
  }

}
</script>
