<template>
  <topic-list-chalk :topicList="dealList"></topic-list-chalk>
</template>

<script>
import { sortByDate } from '~/utils'
import TopicListChalk from '~/components/TopicListChalk'

export default {
  head () {
    return {
      titleTemplate: '%s - 交易'
    }
  },
  async asyncData ({ app }) {
    const [all4all, exchange, free, dn, tuan] = await Promise.all([
      app.$axios.get(`topics/show.json?node_name=all4all`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=exchange`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=free`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=dn`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=tuan`).then(res => res.data)
    ])

    const dealList = sortByDate([...all4all, ...exchange, ...free, ...dn, ...tuan])

    return {
      dealList
    }
  },
  components: {
    TopicListChalk
  }
}
</script>
