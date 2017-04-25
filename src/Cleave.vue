<template>
  <input ref="input" type="text" @input="updateValue" />
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
    updateValue () {
      this.$emit('input', this.$el.value)
      this.$emit('rawValueChanged', this.cleave.getRawValue())
    },
  },

  mounted () {
    this.cleave = new Cleave(this.$el, this.options)
    Object.keys(this.events).map((key) => {
      this.$refs.input.addEventListener(key, this.events[key])
    })
    if (this.options.maxLength) {
      this.$el.setAttribute('maxlength', this.options.maxLength)
    }
  },

  beforeDestroy () {
    this.cleave.destroy()
  },

  watch: {
    options: {
      deep: true,
      handler (val) {
        this.cleave.destroy()
        this.cleave = new Cleave(this.$el, val)
      }
    }
  },

}
</script>
