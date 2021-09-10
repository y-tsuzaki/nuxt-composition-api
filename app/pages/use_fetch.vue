<template>
  <div>
    <h1>Blog posts</h1>
    <template v-if="$fetchState.pending">
      <content-placeholders>
        <content-placeholders-text :lines="20"/>
      </content-placeholders>
    </template>
    <template v-else-if="$fetchState.error">
      <p>Error while fetching posts: {{ $fetchState.error.message }}</p>
    </template>
    <template v-else>
      <ul>
        <li v-for="post of posts" :key="post.id">
          <n-link :to="`/posts/${post.id}`">
            {{ post.title }}
          </n-link>
        </li>
        <li>
          <n-link to="/posts/404">
            404 post
          </n-link>
        </li>
      </ul>
    </template>
  </div>
</template>

<script lang="ts">
import {defineComponent, ref, useFetch} from "@nuxtjs/composition-api";
import {$axios} from "~/app/utils/api";
import Author from "~/app/components/Author.vue";


export default defineComponent({
  components: {Author},
  setup() {
    const posts = ref<any>(null)

    useFetch(async () => {
      posts.value = await $axios.$get('https://jsonplaceholder.typicode.com/posts')
          .then((posts: any[]) => posts.slice(0, 20))
    })

    return {posts}
  },
})


</script>

<style scoped>

</style>
