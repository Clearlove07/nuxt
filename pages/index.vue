<template>
  <section class="container">
    <div>
      <Search @search="searchHandle" />
      <List :list="searchResult" />
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import config from '~/static/config'
import Search from '~/components/track/Search'
import List from '~/components/track/List'

export default {
  components: {
    Search,
    List
  },

  data() {
    return {
      list: [],
      searchResult: [],
      message: 'test'
    }
  },

  mounted() {
    this.getSiteList()
  },

  methods: {
    getSiteList() {
      let url = `${config.host}/site/site/getviewlists`
      let accesstoken = config.user.token
      let offset = 0
      let limit = 10

      axios
        .get(url, {
          params: {
            accesstoken,
            offset,
            limit
          }
        })
        .then(({ data: { code, data } }) => {
          if (code === 0) {
            let { lists } = data
            this.list = lists
          }
        })
    },

    searchHandle(lists) {
      this.searchResult = lists || []
    }
  }
}
</script>

<style>
.container {
  width: 100%;
}
</style>
