<template>
  <v-form ref="form" class="addform" @submit.prevent="createTask">
    <v-text-field
      variant="outlined"
      label="Task"
      placeholder="What task do you need to complete?"
      hint="Hit enter ↵ to add your task."
      persistent-hint
      v-model="text"
    ></v-text-field>
  </v-form>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

import { useStore } from "@/store";
import { TodoItem } from "@/store/state";
import { MutationType } from "@/store/mutations";

export default defineComponent({
  setup() {
    const text = ref("");
    const store = useStore();

    const createTask = () => {
      if (text.value === "") return;

      const item: TodoItem = {
        id: Date.now(),
        text: text.value,
        completed: false,
      };
      store.commit(MutationType.CreateItem, item);
      text.value = "";
    };
    return { createTask, text };
  },
});
</script>
