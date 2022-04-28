<template>
  <template v-if="items.length">
    <TodoItem v-for="item in items" :key="item" v-bind="item" />
  </template>
  <template v-else>
    <p class="placeholder">No tasks 😊</p>
  </template>
</template>

<script lang="ts">
import { computed, defineComponent } from "vue";
import { useStore } from "@/store";
import TodoItem from "./TodoItem.vue";

export default defineComponent({
  components: { TodoItem },
  setup() {
    const store = useStore();
    const items = computed(() => store.state.items);
    return { items };
  },
});
</script>
