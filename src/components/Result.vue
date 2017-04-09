<template>
  <div class="result">
  </div>
</template>

<script>
import punycode from 'punycode'

export default {
  name: 'result',
  props: ['domain', 'tld'],
  data () {
    return {
      result: undefined
    }
  },
  created () {
    // TODO: set domain/tld props
    // TODO: start search domain

    console.log(this.domain)
    // this.tld =
    // this.domain = this.label()
  },
  watch: {
    // TODO: monitor search result
  },
  computed: {
    label () {
      let trimed = this.domain && this.domain.trim()
      if (!trimed) {
        return
      }

      let ascii = punycode.toASCII(trimed)

      let re = new RegExp('^(.*)\\.' + this.tld + '$', 'i')
      let match = re.exec(ascii)
      if (match !== null) {
        ascii = match[1]
      }

      return ascii
    }
  },
  methods: {
    search () {
      const url = 'http://203.141.128.87/perl/domain_check/dm_check_domain.cgi'
      this.$jsonp(url, { domain: this.label })
        .then(json => {
          console.log(json)  // TODO: remove
          return json !== null && json.status === '0'
        })
        .catch(err => {
          console.log(err)  // TODO: remove
        })
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
