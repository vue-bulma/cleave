<template>
  <input type="text" v-bind:value="value" @input="updateValue($event.target.value)" />
</template>

<script>
import Cleave from 'cleave.js'

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
  
  methods: {
    updateValue(value) {
      this.$emit('input', value);
    },
  },

  mounted () {
    this.cleave = new Cleave(this.$el, this.options)
  },

  beforeDestroy () {
    this.cleave.destroy()
  }

}
</script>
