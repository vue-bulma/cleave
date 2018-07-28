# Cleave

Cleave component is based on [cleave.js](https://github.com/nosir/cleave.js) for Vue Bulma.


## Installation

```
$ npm install vue-cleave --save
```

## Examples

```vue
<template>
  <cleave placeholder="Enter your credit card number" ref="creditcard" :options="{ creditCard: true }"></cleave>
</template>

<script>
import Cleave from 'vue-cleave'

export default {
  components: {
    Cleave
  }
}
</script>
```
### Access format free variable for a POST request
```
this.$refs.creditcard.cleave.getRawValue()
```

## Badges

![](https://img.shields.io/badge/license-MIT-blue.svg)
![](https://img.shields.io/badge/status-stable-green.svg)

---

> [fundon.me](https://fundon.me) &nbsp;&middot;&nbsp;
> GitHub [@fundon](https://github.com/fundon) &nbsp;&middot;&nbsp;
> Twitter [@_fundon](https://twitter.com/_fundon)
