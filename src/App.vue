<template>
  <div>
    <div>
      <textarea
        type="text"
        placeholder="Enter some text"
        v-model="message"
      ></textarea>
      <br />
      <button>Add</button>
    </div>
    <div>
      <ul>
        <li v-for="(item, index) in list" :key="index">
          <div v-if="!item.edit">
            <p>{{ item.text }}</p>
            <button>Edit</button>
          </div>
          <div v-else>
            <textarea></textarea>
            <br />
            <button>Save</button>
          </div>
          <button>Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface IlistItem {
  text: string;
  edit: boolean;
}

const message = ref("");
const list = ref<IlistItem[]>([]);

const addItem = (newItem: IlistItem) => {
  return;
};

const deleteItem = (i: number) => {
  return;
};

const editItem = (i: number) => {
  return;
};

const saveItem = (i: number) => {
  return;
};
</script>

<style lang="scss">
#app {
}
</style>
