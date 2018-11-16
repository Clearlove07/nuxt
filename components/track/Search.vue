<template>
  <div class="mainer">
    <div class="search">
      <input 
        v-model="keyword" 
        type="text" 
        name="value" 
        class="input" 
        placeholder="请输入官网名称"
      >
      <button 
        class="btn" 
        @click="search"
      >
        搜索
      </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import config from '~/static/config'

export default {
  data() {
    return {
      keyword: ''
    }
  },

  watch: {
    keyword(curr, old) {}
  },

  mounted() {},

  methods: {
    search() {
      let keyword = this.keyword
      if(!keyword) return
      this.searchSite(keyword)  
    },

    searchSite(keyword) {
      let url = `${config.host}/site/home/searchlist`,
        accesstoken = config.user.token,
        offset = 0,
        limit = 10

      axios
        .get(url, {
          params: {
            keyword,
            accesstoken,
            offset,
            limit
          }
        })
        .then(({ data: { code, data } }) => {
          if (code === 0) {
            let { lists } = data
            this.$emit('search', lists)
          }
        })
    }
  }
}
</script>
<style scoped>
.mainer {
  width: 100%;
}

.search {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 0.6rem;
  width: 100%;
  height: 3rem;
  background-color: #efeff4;
}

.search .input {
  flex-grow: 1;
  padding: 0.3rem 0.6rem;
  height: 2rem;
  border: 0;
  border-radius: 0.5rem;
  background-color: #fff;
  font-size: 1rem;
  text-align: center;
}

.search .btn {
  margin-left: 0.5rem;
  height: 2rem;
  border: 0;
  border-radius: 0.5rem;
}
</style>
