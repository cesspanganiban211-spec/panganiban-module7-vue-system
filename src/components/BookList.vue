<template>
  <div class="bg-white rounded-lg shadow p-6">
    <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-3 mb-4">
      <h2 class="text-lg font-semibold text-gray-800">Book Records <span class="text-sm font-normal text-gray-500">({{ books.length }} total)</span></h2>
      <input v-model="searchTerm" type="text" placeholder="Search by title..." class="border border-gray-300 rounded-md px-3 py-2 w-full sm:w-64 focus:outline-none focus:ring-2 focus:ring-blue-500" />
    </div>

    <div v-if="filteredBooks.length === 0" class="text-center text-gray-500 py-8">No books found.</div>

    <div v-else class="overflow-x-auto">
      <table class="w-full text-sm text-left">
        <thead class="bg-gray-100 text-gray-600 uppercase text-xs">
          <tr>
            <th class="px-4 py-2">Title</th>
            <th class="px-4 py-2">Author</th>
            <th class="px-4 py-2">Category</th>
            <th class="px-4 py-2">Status</th>
            <th class="px-4 py-2 text-right">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="book in filteredBooks" :key="book.id" class="border-b hover:bg-gray-50">
            <td class="px-4 py-2 font-medium text-gray-800">{{ book.title }}</td>
            <td class="px-4 py-2">{{ book.author }}</td>
            <td class="px-4 py-2">{{ book.category }}</td>
            <td class="px-4 py-2">
              <span :class="book.status === 'Available' ? 'bg-green-100 text-green-700' : 'bg-yellow-100 text-yellow-700'" class="px-2 py-1 rounded-full text-xs font-medium">{{ book.status }}</span>
            </td>
            <td class="px-4 py-2 text-right space-x-2">
              <button @click="$emit('edit-book', book)" class="text-blue-600 hover:underline text-sm">Edit</button>
              <button @click="$emit('delete-book', book.id)" class="text-red-600 hover:underline text-sm">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({ books: { type: Array, required: true } })
defineEmits(['edit-book', 'delete-book'])

const searchTerm = ref('')
const filteredBooks = computed(() => {
  const keyword = searchTerm.value.toLowerCase().trim()
  if (!keyword) return props.books
  return props.books.filter(book => book.title.toLowerCase().includes(keyword))
})
</script>