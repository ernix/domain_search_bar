<template>
  <div class="result">
    <span>{{ label }}.{{ tld }}</span>

    <span v-if="typeof result === 'undefined'">
      loading...
    </span>
    <span v-else-if="!result">
      Not available
    </span>
    <span v-else>
      Available!
    </span>

  </div>
</template>

<script>
import punycode from 'punycode'

export default {
  name: 'result',
  props: {
    domain: {
      type: String,
      required: true
    },
    tld: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      result: undefined
    }
  },
  created () {
    this.search()
  },
  computed: {
    label () {
      let trimed = this.domain && this.domain.trim()
      if (!trimed) {
        return
      }

      let ascii = punycode.toASCII(trimed).toLowerCase()

      // Trim trailing tld part from input if exists
      let dtld = '.' + this.tld
      if (ascii.substr(0 - dtld.length) === dtld) {
        ascii = ascii.slice(0, 0 - dtld.length)
      }

      return ascii
    }
  },
  methods: {
    search () {
      let self = this
      const url = 'http://203.141.128.87/perl/domain_check/dm_check_domain.cgi'

      self.$jsonp(url, { domain: self.label + '.' + self.tld })
        .then(json => {
          self.result = json !== null && json.status === '0'
        })
        .catch(err => {
          console.log(err)
          self.result = null
        })
    }
  }
}
</script>

<style lang="scss" scoped>
/* TODO: style goes here */
</style>
