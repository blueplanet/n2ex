<template>
  <topic-list-chalk :topicList="newList"></topic-list-chalk>
</template>

<script>
import TopicListChalk from '~/components/TopicListChalk'

export default {
  head () {
    return {
      titleTemplate: '%s - 最新'
    }
  },
  async asyncData ({ app }) {
    const { data } = await app.$axios.get(`topics/latest.json`)

    return {
      newList: data
    }
  },
  components: {
    TopicListChalk
  }
}
</script>
