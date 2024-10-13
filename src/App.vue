<script setup>
import { ref } from "vue";
const header = ref("Shopping List App");

const items = ref([
  { id: 1, label: "10 party hats" },
  { id: 2, label: "2 board games" },
  { id: 3, label: "20 cups" },
]);

const newItem = ref("");
const newItemPriority = ref("low");
const newItemHighPriority = ref(false);
const iceCreamFlavors = ref(["vanilla"]);
</script>

<template>
  <h1>{{ header }}</h1>
  <input type="text" placeholder="Add an Item" v-model.lazy="newItem" />
  {{ newItem }} <br />
  Priority:
  <label>
    <input type="radio" value="low" v-model="newItemPriority" /> Low
  </label>
  <label>
    <input type="radio" value="hight" v-model="newItemPriority" /> Hight
  </label>
  <br />
  {{ newItemPriority }}
  <br />
  <label>
    Priority:
    <select v-model="newItemPriority">
      <option value="low">Low</option>
      <option value="hight">Hight</option>
    </select> </label
  ><br />
  <label>
    <input type="checkbox" v-model="newItemHighPriority" /> Hight Priority
  </label>
  <br />
  {{ newItemHighPriority }} <br />
  <label>
    <input type="checkbox" value="vanilla" v-model="iceCreamFlavors" /> Vanilla
  </label>
  <label>
    <input type="checkbox" value="chocolate" v-model="iceCreamFlavors" />
    Chocolate
  </label>
  <label>
    <input type="checkbox" value="strawberry" v-model="iceCreamFlavors" />
    Strawberry
  </label>
  <br />
  {{ iceCreamFlavors }}
  <ul>
    <li v-for="{ id, label } in items" :key="id">{{ label }}</li>
  </ul>
</template>
