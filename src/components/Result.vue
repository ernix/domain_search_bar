<template>
  <div class="result">
  </div>
</template>

<script>
import punycode from 'punycode'

export default {
  name: 'result',
  data () {
    return {
      domain: 'foobar.earth',
      result: undefined
    }
  },
  created () {
  },
  watch: {
  },
  computed: {
    label () {
      let label = punycode.toASCII(this.domain.replace(/^\s*|\s*$/, '', 'g'))

      let m = (/^(.*)\.earth$/i).exec(label)
      if (m !== null) {
        label = m[1]
      }

      return label
    }
  },
  methods: {
    search () {
      const url = 'http://domain.earth/domain_search/earth.cgi'
      this.$jsonp(url, { domain: this.label })
        .then(json => {
        })
        .catch(err => {
          console.log(err)
        })
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
