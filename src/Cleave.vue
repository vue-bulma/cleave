<template>
  <input ref="input" type="text" v-bind:value="value" @input="updateValue($event.target.value)" />
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
    },
    events: {
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
    Object.keys(this.events).map((key) => {
        this.$refs.input.addEventListener(key, this.events[key])
    })
  },

  beforeDestroy () {
    this.cleave.destroy()
  }

}
</script>
