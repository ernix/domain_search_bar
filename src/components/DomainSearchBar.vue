<template>
  <div class="domain-search-bar">

    <form @submit.prevent="add">
      <input v-model="next" name="domain" type="text" />
      <button name="submit" type="submit">search</button>
    </form>

    <result
      v-for="result in results"
      v-bind="result"
      :key="result.domain"
      ></result>

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
    const TLD = 'earth'

    return {
      next: '',
      tld: TLD,
      results: []
    }
  },
  methods: {
    add (e) {
      this.results.unshift({
        domain: this.next,
        tld: this.tld
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
