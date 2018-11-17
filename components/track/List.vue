<template>
  <div class="list">
    <div 
      v-for="(site, index) in list" 
      :key="site.sid"
      class="list__item" 
    >
      <div class="site__logo">
        <image :src="site.logo" />
      </div>
      <div class="site__info">
        <div class="site__info__name">{{ site.name }}</div>
        <div class="btns">
          <i v-if="site.istop == 1" @click="setTop(index)" class="el-icon-star-on" />
          <i v-else @click="setTop(index)" class="el-icon-star-off" />
          <i class="el-icon-delete" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import config from '~/static/config'

export default {
  props: {
    list: {
      type: Array,
      default: function() {
        return []
      }
    }
  },

  data() {
    return {
      lists: []
    }
  },

  methods: {
    setTop(index) {
      let { istop, sid } = this.list[index]
      this.toggleTop(index, istop, sid)
    },

    toggleTop(index, istop, sid) {
      let op = +istop ? 'cancel' : 'set',
        url = `${config.host}/site/home/settop`,
        accesstoken = config.user.token
      axios({
          url,
          method: 'post',
          params: {
            accesstoken
          }, data: {
            sid, op
          }
        })
        .then(({ data: { code, data } }) => {
          if (code === 0) {
            this.list[index].istop = !(+istop)
          }
        })
    }
  }
}
</script>

<style scoped>
.list__item {
  display: flex;
}

.site__logo {
  padding: 1rem 1.25rem;
  border-bottom: 0.06rem solid #fff;
}

.site__logo image {
  width: 3.12rem;
  height: 3.12rem;
  border-radius: 50%;
}

.site__info {
  flex-grow: 1;
  display: flex;
  justify-content: space-between;
  align-content: center;
  padding: 1.25rem 1.25rem 1.25rem 0;
  border-bottom: 0.06rem solid #e5e5e5;
}

.site__info__name {
  font-size: 1rem;
  color: #000;
}

.btns i {
  padding: 0.3rem 0.4rem;
}
</style>
