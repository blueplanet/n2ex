<template>
  <topic-list-chalk :topicList="creativeList"></topic-list-chalk>
</template>

<script>
import { sortByDate } from '~/utils'
import TopicListChalk from '~/components/TopicListChalk'

export default {
  head () {
    return {
      titleTemplate: '%s - 创意'
    }
  },
  async asyncData ({ app }) {
    const [create, design, ideas] = await Promise.all([
      app.$axios.get(`topics/show.json?node_name=create`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=design`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=ideas`).then(res => res.data)
    ])

    const creativeList = sortByDate([...create, ...design, ...ideas])

    return {
      creativeList
    }
  },
  components: {
    TopicListChalk
  }
}
</script>
