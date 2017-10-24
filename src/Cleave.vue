<template>
  <input ref="input" type="text" />
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
    emitEvent () {
      this.$emit('input', this.$el.value)
      this.$emit('rawValueChanged', this.cleave.getRawValue())
    }
  },

  mounted () {
    this.$el.value = this.value
    this.cleave = new Cleave(this.$el, this.options)
    Object.keys(this.events).forEach((key) => {
      this.$refs.input.addEventListener(key, this.events[key])
    })
    if (this.options.maxLength) {
      this.$el.setAttribute('maxlength', this.options.maxLength)
    }

    // in case of cleave.js remove result or properties from cleave instance.
    if (this.cleave.properties && this.cleave.properties.hasOwnProperty('result')) {
      this.$watch('cleave.properties.result', this.emitEvent)
    } else {
      this.$el.addEventListener('input', this.emitEvent)
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
