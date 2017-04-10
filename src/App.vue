<template>
  <div id="domain-search-bar">

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
import Vue from 'vue'
import VueJsonp from 'vue-jsonp'
Vue.use(VueJsonp)

import Result from './components/Result'

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

<style lang="scss">
#domain-search-bar {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
