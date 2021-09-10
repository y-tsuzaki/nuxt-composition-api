<template>
  <div>
    <ul>
      <li v-for="(todo, index) in todos">
        <label>
          <input type="checkbox" v-model="todo.done"/>
        </label>
        <span>{{ todo.title }}</span>
        <button @click="remove(index)">REMOVE</button>
      </li>
    </ul>
    <label>
      <input type="text" v-model="newToDoTitle"/>
    </label>
    <button @click="add">ADD</button>
    <br><br>
    <n-link to="use_fetch">useFetchExample</n-link>
  </div>
</template>

<script lang="ts">
import {defineComponent, ref} from "@nuxtjs/composition-api";
import Author from "~/app/components/Author.vue";

type ToDo = {
  done: boolean,
  title: string
}

export default defineComponent({
  components: {Author},
  head: {
    title: 'My Page'
  },
  setup() {
    const todos = ref<ToDo[]>([
      {
        done: false,
        title: 'これはやることです'
      }, {
        done: true,
        title: '二つ目のやること'
      }, {
        done: false,
        title: '三つ目のやること'
      },
    ])
    const newToDoTitle = ref<string>('')
    const add = () => {
      todos.value.push(
          {
            done: false,
            title: newToDoTitle.value
          }
      )
      newToDoTitle.value = ''
    }
    const remove = (index: number) => {
      todos.value.splice(index, 1);
    }

    return {
      todos,
      newToDoTitle,
      add,
      remove
    }
  }
})
</script>
