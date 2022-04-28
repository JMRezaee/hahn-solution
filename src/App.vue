<template>
  <v-app>
    <div class="main">
      <div class="board">
        <div class="board__header">
          <h3>Easy todo list like others!</h3>
          <p v-if="loading">Loading...</p>
          <p v-else>{{ completedCount }} of {{ totalCount }} completed.</p>
        </div>
        <div class="board__body" v-if="!loading">
          <NewItem />
          <TodoList />
        </div>
        <div class="board__footer"></div>
      </div>
    </div>
  </v-app>
</template>

<script lang="ts">
import { computed, defineComponent, onMounted } from "vue";

import NewItem from "./components/NewItem.vue";
import TodoList from "./components/TodoList.vue";
import { useStore } from "./store";
import { ActionTypes } from "./store/actions";

export default defineComponent({
  components: { NewItem, TodoList },
  setup() {
    const store = useStore();

    const loading = computed(() => store.state.loading);
    onMounted(() => store.dispatch(ActionTypes.GetTodoItems));

    const completedCount = computed(() => store.getters.completedCount);
    const totalCount = computed(() => store.getters.totalCount);

    return { loading, completedCount, totalCount };
  },
});
</script>

<style lang="scss">
@import "./assets/scss/main.scss";
</style>
