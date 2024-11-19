<script setup>
import { ref } from 'vue'

const userItems = ref([
  { id: 1, name: "Shoes 1" },
  { id: 2, name: "Shoes 2" },
  { id: 3, name: "Shoes 3" },
  { id: 4, name: "Shoes 4" },
  { id: 5, name: "T-shirt 1" },
  { id: 6, name: "T-shirt 2" },
  { id: 7, name: "T-shirt 3" },
  { id: 8, name: "T-shirt 4" }
])

const availableItems = ref([
  { id: 11, name: "Jacket 1" },
  { id: 12, name: "Jacket 2" },
  { id: 13, name: "Jacket 3" },
  { id: 14, name: "Jacket 4" },
  { id: 15, name: "Hoodie 1" },
  { id: 16, name: "Hoodie 2" },
  { id: 17, name: "Hoodie 3" },
  { id: 18, name: "Hoodie 4" }
])

const selectedUserItems = ref([])
const selectedAvailableItem = ref(null)

const selectUserItem = (item) => {
  if (selectedUserItems.value.length < 6 && !selectedUserItems.value.includes(item)) {
    selectedUserItems.value.push(item)
  }
}

const selectAvailableItem = (item) => {
  selectedAvailableItem.value = item
}

const removeSelectedUserItem = (index) => {
  selectedUserItems.value.splice(index, 1)
}
</script>

<template>
  <div class="container">
    <!-- Top Section -->
    <div class="top-section">
      <!-- Selected User Items -->
      <div class="selected-items">
        <h2>Selected User Items</h2>
        <div class="items-grid">
          <div v-for="(item, index) in selectedUserItems" 
               :key="item.id" 
               class="item"
               @click="removeSelectedUserItem(index)">
            {{ item.name }}
          </div>
        </div>
      </div>

      <!-- Selected Available Item -->
      <div class="selected-items">
        <h2>Selected Available Item</h2>
        <div class="item" v-if="selectedAvailableItem">
          {{ selectedAvailableItem.name }}
        </div>
      </div>
    </div>

    <!-- Bottom Section -->
    <div class="bottom-section">
      <!-- User Items -->
      <div class="items-container">
        <h2>User Items</h2>
        <div class="items-grid">
          <div v-for="item in userItems" 
               :key="item.id" 
               class="item"
               :class="{ 'selected': selectedUserItems.includes(item) }"
               @click="selectUserItem(item)">
            {{ item.name }}
          </div>
        </div>
      </div>

      <!-- Available Items -->
      <div class="items-container">
        <h2>Available Items</h2>
        <div class="items-grid">
          <div v-for="item in availableItems" 
               :key="item.id" 
               class="item"
               :class="{ 'selected': selectedAvailableItem === item }"
               @click="selectAvailableItem(item)">
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

.top-section, .bottom-section {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.selected-items, .items-container {
  flex: 1;
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 8px;
}

.items-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: 10px;
  margin-top: 10px;
}

.item {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: center;
  cursor: pointer;
  border-radius: 4px;
  background-color: #f5f5f5;
}

.item:hover {
  background-color: #e0e0e0;
}

.item.selected {
  background-color: #4CAF50;
  color: white;
}

h2 {
  margin: 0 0 10px 0;
  font-size: 1.2em;
}
</style>