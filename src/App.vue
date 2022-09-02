<template>
  <div>
    <div>
      <textarea
        type="text"
        placeholder="Enter some text"
        v-model="message"
      ></textarea>
      <br />
      <button @click="addItem(message)">Add</button>
    </div>
    <div>
      <ul>
        <li v-for="(item, index) in list" :key="index">
          <div v-if="!item.edit">
            <p>{{ item.text }}</p>
            <button @click="editItem(index)">Edit</button>
          </div>
          <div v-else>
            <textarea v-model="item.text"></textarea>
            <br />
            <button @click="saveItem(index)">Save</button>
          </div>
          <br />
          <button @click="deleteItem(index)">Delete</button>
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

const addItem = (newItem: string) => {
  list.value.push({ text: newItem, edit: false });
  message.value = "";
};

const deleteItem = (i: number) => {
  list.value.splice(i, 1);
};

const editItem = (i: number) => {
  list.value[i].edit = true;
};

const saveItem = (i: number) => {
  list.value[i].edit = false;
};
</script>

<style lang="scss">
#app {
}
</style>
