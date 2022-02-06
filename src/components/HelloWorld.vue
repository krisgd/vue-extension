<template>
  <div>
    <p>{{ defaultText }}</p>
    <button @click="getInfo">Get Info</button>
    <div>
      <pre>
        {{ info }}
      </pre>
    </div>
  </div>
</template>

<script>
const qs = require('qs')

export default {
  name: 'HelloWorld',
  mounted() {
    browser.runtime.sendMessage({})
  },
  computed: {
    defaultText() {
      return browser.i18n.getMessage('extName')
    },
  },
  data() {
    return {
      info: '',
    }
  },
  methods: {
    async getInfo() {
      const response = await fetch('http://localhost:3000/api/get-info', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
        },
        body: qs.stringify({
          url: 'https://www.youtube.com/watch?v=G7_rYqcTzYY',
        }),
      })

      const info = await response.json()

      this.info = info
    },
  },
}
</script>

<style scoped>
p {
  font-size: 20px;
}
</style>
