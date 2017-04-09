<template>
  <div class="domain-search-bar">

    <form @submit.prevent>
      <input v-model="tld" name="tld" type="hidden" />
      <input v-model="next" name="domain" type="text" />
      <button @click="add" name="submit" type="submit">search</button>
    </form>

    <div v-for="domain in domains" :is="domain.type">
      <result :tld="domain.tld" :domain="domain.domain" ></result>
    </div>

  </div>
</template>

<script>
import Result from './Result'

export default {
  name: 'domain-search-bar',
  components: {
    Result
  },
  data () {
    return {
      next: '',
      tld: '',
      domains: []
    }
  },
  methods: {
    add (e) {
      this.domains.push({
        domain: this.next,
        tld: this.tld,
        type: 'Result'
      })

      this.next = ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
/* TODO: style goes here */
</style>
