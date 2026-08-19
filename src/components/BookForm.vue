<template>
  <div class="bg-white rounded-lg shadow p-6 mb-6">
    <h2 class="text-lg font-semibold text-gray-800 mb-4">{{ editingId ? "Edit Book" : "Add a New Book" }}</h2>
    <form @submit.prevent="handleSubmit" class="grid grid-cols-1 sm:grid-cols-2 gap-4">
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">Title</label>
        <input v-model="form.title" type="text" class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500" />
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">Author</label>
        <input v-model="form.author" type="text" class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500" />
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">Category</label>
        <input v-model="form.category" type="text" placeholder="e.g. Fiction, Reference" class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500" />
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1">Status</label>
        <select v-model="form.status" class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500">
          <option value="Available">Available</option>
          <option value="Borrowed">Borrowed</option>
        </select>
      </div>

      <p v-if="errorMessage" class="sm:col-span-2 text-sm text-red-600 bg-red-50 border border-red-200 rounded-md px-3 py-2">{{ errorMessage }}</p>
      <p v-if="successMessage" class="sm:col-span-2 text-sm text-green-700 bg-green-50 border border-green-200 rounded-md px-3 py-2">{{ successMessage }}</p>

      <div class="sm:col-span-2 flex gap-3">
        <button type="submit" class="bg-blue-700 text-white px-4 py-2 rounded-md hover:bg-blue-800 transition">{{ editingId ? "Update Book" : "Add Book" }}</button>
        <button v-if="editingId" type="button" @click="cancelEdit" class="bg-gray-200 text-gray-700 px-4 py-2 rounded-md hover:bg-gray-300 transition">Cancel</button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({ editingBook: { type: Object, default: null } })
const emit = defineEmits(['add-book', 'update-book', 'cancel-edit'])

const emptyForm = { title: '', author: '', category: '', status: 'Available' }
const form = ref({ ...emptyForm })
const editingId = ref(null)
const errorMessage = ref('')
const successMessage = ref('')

watch(() => props.editingBook, (book) => {
  if (book) {
    form.value = { ...book }
    editingId.value = book.id
  }
})

function handleSubmit() {
  errorMessage.value = ''
  successMessage.value = ''

  if (!form.value.title.trim() || !form.value.author.trim() || !form.value.category.trim()) {
    errorMessage.value = 'Please fill in Title, Author, and Category before submitting.'
    return
  }

  if (editingId.value) {
    emit('update-book', { ...form.value, id: editingId.value })
    successMessage.value = 'Book updated successfully.'
  } else {
    emit('add-book', { ...form.value })
    successMessage.value = 'Book added successfully.'
  }

  form.value = { ...emptyForm }
  editingId.value = null
  setTimeout(() => { successMessage.value = '' }, 2500)
}

function cancelEdit() {
  form.value = { ...emptyForm }
  editingId.value = null
  emit('cancel-edit')
}
</script>