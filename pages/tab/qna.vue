<template>
  <topic-list-chalk :topicList="qnaList"></topic-list-chalk>
</template>

<script>
import TopicListChalk from '~/components/TopicListChalk'

export default {
  head () {
    return {
      titleTemplate: '%s - 问与答'
    }
  },
  async asyncData ({ app }) {
    const { data } = await app.$axios.get(`topics/show.json?node_name=qna`)

    return {
      qnaList: data
    }
  },
  components: {
    TopicListChalk
  }
}
</script>
