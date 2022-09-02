<template>
  <div>
    <div v-if="!props.item.edit">
      <p>{{ props.item.text }}</p>
      <button @click="handleAction('edit', props.index)">Edit</button>
    </div>
    <div v-else>
      <textarea v-model="userInput" @input="handleUserInput"></textarea>
      <button @click="handleAction('save', props.index)">Save</button>
    </div>
    <button @click="handleAction('delete', props.index)">Delete</button>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, ref } from "vue";
import { IlistItem } from "./NoteList.vue";

export interface IProps {
  item: IlistItem;
  index: number;
  modelValue: string;
}

const props = defineProps<IProps>();
const emit = defineEmits(["handleAction", "update:modelValue"]);

const userInput = ref(props.modelValue);

const handleAction = (action: string, index: number) => {
  emit("handleAction", action, index);
};

const handleUserInput = (e: Event) => {
  const target = e.target as HTMLInputElement;

  emit("update:modelValue", target.value);
};
</script>
