<template>
  <input :type="type" v-model="value" />
</template>

<script>
import Cleave from 'cleave.js'

export default {
  props: {
    type: {
      type: String,
      default: 'text'
    },
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
