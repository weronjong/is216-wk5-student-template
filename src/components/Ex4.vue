<script setup>
import { ref } from 'vue'
const items = ref(['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'])
const newItem = ref('')

function addItem() {
    if (newItem.value.trim() !== '') {
        items.value.push(newItem.value.trim())
        newItem.value = ''
    }
}

function removeItem(index) {
    items.value.splice(index, 1)
}
</script>

<template>

    <h2>Shopping Cart</h2>
    <input v-model="newItem" @keyup.enter="addItem" placeholder="Add item">
    <button @click="addItem">Add</button>
    <ul>
        <li v-for="(item, index) in items" :key="item">
            {{ item }}
            <button @click="removeItem(index)">Remove</button>
        </li>
    </ul>

</template>
