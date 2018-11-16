<template>
  <div class="list">
    <div class="list__item" v-for="site in list" :key="site.sid">
      <div class="site__logo">
        <image :src="site.logo" />
      </div>
      <div class="site__info">
        <div class="site__info__name">{{ site.name }}</div>
        <i class="el-icon-edit"></i>
      </div>
    </div>
  </div>
</template>

<script>
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
</style>