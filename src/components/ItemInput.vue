<template>
  <div>
    <textarea
      v-model.lazy="input"
      @input="addItem"
      type="text"
      placeholder="Enter some text"
    >
    </textarea>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, ref } from "vue";

export interface IProps {
  message: string;
}

const props = defineProps<IProps>();
const emit = defineEmits(["update:modelValue"]);

const input = ref(props.message);

const addItem = (e: Event) => {
  const target = e.target as HTMLInputElement;

  emit("update:modelValue", target.value);
};
</script>
