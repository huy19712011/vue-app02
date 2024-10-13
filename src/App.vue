<script setup>
import { ref } from "vue";
const header = ref("Shopping List App");

const items = ref([
  // { id: 1, label: "10 party hats" },
  // { id: 2, label: "2 board games" },
  // { id: 3, label: "20 cups" },
]);

const newItem = ref("");
const newItemPriority = ref("low");
const newItemHighPriority = ref(false);
const editing = ref(false);
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value });
  newItem.value = "";
};
const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};
</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">
      Add Item
    </button>
  </div>
  <a v-bind:href="newItem">Dynamic Link</a>
  <form class="add-item-form" v-on:submit.prevent="saveItem" v-if="editing">
    <input type="text" placeholder="Add an Item" v-model.lazy="newItem" />

    <label>
      <input type="checkbox" v-model="newItemHighPriority" /> Hight Priority
    </label>
    <button class="btn btn-primary">Save Item</button>
  </form>
  <ul>
    <li v-for="{ id, label } in items" :key="id">{{ label }}</li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>
</template>
