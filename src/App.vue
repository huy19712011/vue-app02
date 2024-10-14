<script setup>
import { ref } from "vue";
const header = ref("Shopping List App");

const items = ref([
  { id: 1, label: "10 party hats", purchased: true, hightPriority: false },
  { id: 2, label: "2 board games", purchased: true, hightPriority: false },
  { id: 3, label: "20 cups", purchased: false, hightPriority: true },
]);

const newItem = ref("");
const newItemPriority = ref("low");
const newItemHighPriority = ref(false);
const editing = ref(false);
const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    hightPriority: newItemHighPriority.value,
  });
  newItem.value = "";
  newItemHighPriority.value = false;
};
const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};
const togglePurchased = (item) => {
  item.purchased = !item.purchased;
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
  <form class="add-item-form" v-on:submit.prevent="saveItem" v-if="editing">
    <input type="text" placeholder="Add an Item" v-model.lazy="newItem" />

    <label>
      <input type="checkbox" v-model="newItemHighPriority" /> Hight Priority
    </label>
    <button class="btn btn-primary" v-bind:disabled="newItem.length < 3">
      Save Item
    </button>
  </form>
  <ul>
    <li
      v-for="({ id, label, purchased, hightPriority }, index) in items"
      @click="togglePurchased(items[index])"
      :key="id"
      :class="{
        strikeout: purchased,
        priority: hightPriority,
        'static-class': true,
      }"
    >
      {{ label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>
</template>
