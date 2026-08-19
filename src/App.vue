<template>
  <div class="min-h-screen bg-amber-50/50 flex flex-col font-sans text-gray-800">
    <!-- Header -->
    <header class="bg-gradient-to-r from-amber-900 via-amber-800 to-stone-900 text-white py-8 shadow-lg border-b-4 border-amber-600">
      <div class="max-w-5xl mx-auto px-4 flex flex-col md:flex-row items-center justify-between gap-4">
        <div class="flex items-center space-x-3">
          <span class="text-4xl">📚</span>
          <div>
            <h1 class="text-2xl md:text-3xl font-extrabold tracking-tight">CENTRAL LIBRARY SYSTEM</h1>
            <p class="text-amber-200 text-sm font-medium">Module 7 Architecture & Management</p>
          </div>
        </div>
        <!-- Quick Stats Badge -->
        <div class="flex gap-2 bg-amber-950/60 px-4 py-2 rounded-xl border border-amber-700/50 text-xs">
          <div class="text-center px-2 border-r border-amber-800">
            <span class="block text-lg font-bold text-amber-300">{{ books.length }}</span>
            <span class="text-amber-200">Total Books</span>
          </div>
          <div class="text-center px-2 border-r border-amber-800">
            <span class="block text-lg font-bold text-emerald-400">{{ availableCount }}</span>
            <span class="text-amber-200">Available</span>
          </div>
          <div class="text-center px-2">
            <span class="block text-lg font-bold text-amber-400">{{ borrowedCount }}</span>
            <span class="text-amber-200">Borrowed</span>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="flex-1 max-w-5xl w-full mx-auto p-4 md:p-6 space-y-6">
      
      <!-- Add / Edit Book Card -->
      <section class="bg-white p-6 rounded-2xl shadow-md border border-amber-200/60 relative overflow-hidden">
        <div class="absolute top-0 left-0 w-2 h-full bg-amber-700"></div>
        <div class="flex items-center justify-between mb-4">
          <h2 class="text-lg font-bold text-amber-900 flex items-center gap-2">
            <span>{{ isEditing ? '✏️ Edit Book Record' : '📖 Add New Book' }}</span>
          </h2>
          <span v-if="isEditing" class="text-xs bg-amber-100 text-amber-800 px-2 py-1 rounded-full font-semibold">Editing Mode Active</span>
        </div>

        <form @submit.prevent="handleSubmit" class="space-y-4">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-amber-900/70 mb-1">Book Title</label>
              <input v-model="form.title" type="text" placeholder="e.g. Introduction to Algorithms" class="mt-1 block w-full rounded-xl border-gray-300 shadow-sm p-2.5 border focus:ring-amber-600 focus:border-amber-600 text-sm bg-gray-50/50" required />
            </div>
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-amber-900/70 mb-1">Author</label>
              <input v-model="form.author" type="text" placeholder="e.g. Thomas H. Cormen" class="mt-1 block w-full rounded-xl border-gray-300 shadow-sm p-2.5 border focus:ring-amber-600 focus:border-amber-600 text-sm bg-gray-50/50" required />
            </div>
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-amber-900/70 mb-1">Category</label>
              <select v-model="form.category" class="mt-1 block w-full rounded-xl border-gray-300 shadow-sm p-2.5 border focus:ring-amber-600 focus:border-amber-600 text-sm bg-gray-50/50" required>
                <option value="" disabled>Select Category</option>
                <option value="Technology">Technology</option>
                <option value="Education">Education</option>
                <option value="Architecture">Architecture</option>
                <option value="Literature">Literature</option>
              </select>
            </div>
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-amber-900/70 mb-1">Status</label>
              <div class="flex items-center space-x-6 mt-3">
                <label class="inline-flex items-center cursor-pointer">
                  <input type="radio" v-model="form.status" value="Available" class="text-amber-700 border-gray-300 focus:ring-amber-600" />
                  <span class="ml-2 text-sm font-medium text-gray-700">Available</span>
                </label>
                <label class="inline-flex items-center cursor-pointer">
                  <input type="radio" v-model="form.status" value="Borrowed" class="text-amber-700 border-gray-300 focus:ring-amber-600" />
                  <span class="ml-2 text-sm font-medium text-gray-700">Borrowed</span>
                </label>
              </div>
            </div>
          </div>

          <div class="flex space-x-3 pt-2">
            <button type="submit" class="bg-amber-800 hover:bg-amber-900 text-white px-5 py-2.5 rounded-xl text-sm font-semibold shadow-md transition transform active:scale-95">
              {{ isEditing ? 'Update Book Record' : 'Add to Catalog' }}
            </button>
            <button type="button" @click="resetForm" class="bg-stone-200 hover:bg-stone-300 text-stone-700 px-4 py-2.5 rounded-xl text-sm font-semibold transition">
              Clear Form
            </button>
          </div>
        </form>
      </section>

      <!-- Book Catalog Section -->
      <section class="bg-white p-6 rounded-2xl shadow-md border border-amber-200/60">
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-5">
          <h2 class="text-lg font-bold text-amber-900">Library Book Catalog</h2>
          <!-- Search Input -->
          <div class="w-full md:w-72">
            <input v-model="searchQuery" type="text" placeholder="🔍 Search title, author..." class="w-full text-sm rounded-xl border border-gray-300 px-3 py-2 bg-gray-50/50 focus:outline-none focus:ring-2 focus:ring-amber-600" />
          </div>
        </div>

        <div class="overflow-x-auto rounded-xl border border-gray-100">
          <table class="w-full text-left border-collapse">
            <thead>
              <tr class="bg-amber-900/5 text-xs font-bold text-amber-900 uppercase tracking-wider border-b border-gray-200">
                <th class="p-3.5">Title</th>
                <th class="p-3.5">Author</th>
                <th class="p-3.5">Category</th>
                <th class="p-3.5">Status</th>
                <th class="p-3.5 text-center">Actions</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-100 text-sm">
              <tr v-for="book in filteredBooks" :key="book.id" class="hover:bg-amber-50/40 transition">
                <td class="p-3.5 font-semibold text-gray-900">{{ book.title }}</td>
                <td class="p-3.5 text-gray-600">{{ book.author }}</td>
                <td class="p-3.5">
                  <span class="bg-stone-100 text-stone-700 px-2.5 py-1 rounded-lg text-xs font-medium">{{ book.category }}</span>
                </td>
                <td class="p-3.5">
                  <span :class="book.status === 'Available' ? 'bg-emerald-100 text-emerald-800 border border-emerald-200' : 'bg-amber-100 text-amber-800 border border-amber-200'" class="px-2.5 py-1 rounded-full text-xs font-bold inline-flex items-center gap-1">
                    <span class="w-1.5 h-1.5 rounded-full" :class="book.status === 'Available' ? 'bg-emerald-500' : 'bg-amber-500'"></span>
                    {{ book.status }}
                  </span>
                </td>
                <td class="p-3.5 text-center space-x-2">
                  <button @click="editBook(book)" class="bg-sky-600 hover:bg-sky-700 text-white px-3 py-1.5 rounded-lg text-xs font-semibold shadow-sm transition">✏️ Edit</button>
                  <button @click="deleteBook(book.id)" class="bg-rose-600 hover:bg-rose-700 text-white px-3 py-1.5 rounded-lg text-xs font-semibold shadow-sm transition">🗑️ Delete</button>
                </td>
              </tr>
              <tr v-if="filteredBooks.length === 0">
                <td colspan="5" class="p-8 text-center text-gray-400 font-medium">No matching books found in the library catalog.</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const books = ref([])
const isEditing = ref(false)
const editingId = ref(null)
const searchQuery = ref('')

const form = ref({
  title: '',
  author: '',
  category: '',
  status: 'Available'
})

const STORAGE_KEY = 'panganiban-module7-books'

onMounted(() => {
  const saved = localStorage.getItem(STORAGE_KEY)
  if (saved) {
    books.value = JSON.parse(saved)
  } else {
    books.value = [
      { id: 1, title: 'Vue.js 3 Basics', author: 'Evan You', category: 'Technology', status: 'Available' },
      { id: 2, title: 'SE1: Architecture', author: 'Ian Sommerville', category: 'Architecture', status: 'Borrowed' },
      { id: 3, title: 'Tailwind CSS v4', author: 'Adam Wathan', category: 'Technology', status: 'Borrowed' }
    ]
    saveToStorage()
  }
})

// Computed stats & filter
const availableCount = computed(() => books.value.filter(b => b.status === 'Available').length)
const borrowedCount = computed(() => books.value.filter(b => b.status === 'Borrowed').length)

const filteredBooks = computed(() => {
  return books.value.filter(b => 
    b.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
    b.author.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
    b.category.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})

function saveToStorage() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(books.value))
}

function handleSubmit() {
  if (isEditing.value) {
    const index = books.value.findIndex(b => b.id === editingId.value)
    if (index !== -1) {
      books.value[index] = { id: editingId.value, ...form.value }
    }
  } else {
    books.value.push({ id: Date.now(), ...form.value })
  }
  saveToStorage()
  resetForm()
}

function editBook(book) {
  isEditing.value = true
  editingId.value = book.id
  form.value = { title: book.title, author: book.author, category: book.category, status: book.status }
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function deleteBook(id) {
  if (confirm('Are you sure you want to delete this book record?')) {
    books.value = books.value.filter(b => b.id !== id)
    saveToStorage()
  }
}

function resetForm() {
  isEditing.value = false
  editingId.value = null
  form.value = { title: '', author: '', category: '', status: 'Available' }
}
</script>