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
            <button @click="handleItemAction('edit', index)">Edit</button>
          </div>
          <div v-else>
            <textarea v-model="item.text"></textarea>
            <br />
            <button @click="handleItemAction('save', index)">Save</button>
          </div>
          <button @click="handleItemAction('delete', index)">Delete</button>
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

if (window.localStorage.getItem("notes") !== null) {
  list.value = JSON.parse(window.localStorage.getItem("notes") as string);
}

const addItem = (newItem: string) => {
  list.value.push({ text: newItem, edit: false });
  window.localStorage.setItem("notes", JSON.stringify(list.value));
  message.value = "";
};

const handleItemAction = (action: string, i: number) => {
  if (action === "edit") {
    list.value[i].edit = true;
  } else if (action === "save") {
    list.value[i].edit = false;
  } else if (action === "delete") {
    list.value.splice(i, 1);
  }

  window.localStorage.setItem("notes", JSON.stringify(list.value));
};
</script>

<style lang="scss">
#app {
}
</style>
