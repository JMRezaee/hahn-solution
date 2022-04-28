<template>
  <div class="todoitem" :class="completed ? 'border--green' : 'border--white'">
    <div class="todoitem__left">
      <p>{{ text }}</p>
    </div>
    <div class="todoitem__right">
      <v-btn
        class="ma-1"
        size="small"
        icon="mdi-delete"
        color="warning"
        title="Delete Task"
        @click="deleteItem"
      ></v-btn>
      <v-btn
        class="ma-1"
        size="small"
        :icon="completed ? 'mdi-close' : 'mdi-check'"
        :color="completed ? 'error' : 'success'"
        :title="completed ? 'Undo' : 'Done'"
        @click="toggleCompletion"
      ></v-btn>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import { useStore } from "@/store";
import { MutationType } from "@/store/mutations";

export default defineComponent({
  props: {
    id: { type: Number, required: true },
    text: { type: String, required: true },
    completed: { type: Boolean, required: true },
  },
  setup(props) {
    const store = useStore();

    const toggleCompletion = () => {
      store.commit(MutationType.CompleteItem, {
        id: props.id,
        completed: !props.completed,
      });
    };

    const deleteItem = () => {
      store.commit(MutationType.DeleteItem, {
        id: props.id,
      });
    };

    return { toggleCompletion, deleteItem };
  },
});
</script>
