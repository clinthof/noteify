<template>
  <div>
    <div>
      <textarea
        type="text"
        placeholder="Enter some text"
        v-model.lazy="message"
      ></textarea>
      <br />
      <button @click="addItem(message)" :disabled="!message">Add</button>
    </div>
    <div>
      <ul>
        <li v-for="(item, index) in list" :key="index">
          <NoteCard
            :item="item"
            :index="index"
            @handle-action="handleItemAction"
            v-model="item.text"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import NoteCard from "./NoteCard.vue";
import { ref } from "vue";

export interface IlistItem {
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
