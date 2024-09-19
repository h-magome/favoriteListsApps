<template>
    <div class="min-h-screen bg-gray-900 text-white">
      <header class="bg-gray-800 shadow-md" role="banner">
        <div class="container mx-auto px-4 py-6 flex justify-between items-center">
          <h1 class="text-2xl font-bold">My Favorite Places</h1>
          <button class="bg-white text-gray-900 px-4 py-2 rounded-full hover:bg-gray-200 transition duration-300 ease-in-out flex items-center">
            <UserIcon class="w-5 h-5 mr-2" />
            Profile
          </button>
        </div>
      </header>
  
      <main class="container mx-auto px-4 py-8" role="main">
        <div class="flex justify-between items-center mb-8">
          <h2 class="text-3xl font-semibold">My Lists</h2>
          <button @click="showNewListModal = true" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-full transition duration-300 ease-in-out flex items-center">
            <PlusIcon class="w-5 h-5 mr-2" />
            New List
          </button>
        </div>
  
        <div v-if="lists.length === 0" class="text-center py-12">
          <MapIcon class="w-16 h-16 mx-auto mb-4 text-gray-600" />
          <p class="text-xl text-gray-400">You don't have any lists yet.</p>
          <p class="text-gray-500 mt-2">Create a new list to get started!</p>
        </div>
  
        <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div v-for="list in lists" :key="list.id" class="bg-gray-800 rounded-lg shadow-lg overflow-hidden hover:shadow-xl transition duration-300 ease-in-out">
            <div class="p-6">
              <h3 class="text-xl font-semibold mb-2">{{ list.title }}</h3>
              <p class="text-gray-400 mb-4">{{ list.placesCount }} places</p>
              <div class="flex justify-between items-center">
                <button class="text-blue-400 hover:text-blue-300 transition duration-300 ease-in-out flex items-center">
                  <EyeIcon class="w-5 h-5 mr-2" />
                  View
                </button>
                <button class="text-gray-400 hover:text-gray-300 transition duration-300 ease-in-out flex items-center">
                  <ShareIcon class="w-5 h-5 mr-2" />
                  Share
                </button>
              </div>
            </div>
          </div>
        </div>
      </main>
  
      <!-- New List Modal -->
      <div v-if="showNewListModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center" role="dialog" aria-labelledby="modalTitle">
        <div class="bg-gray-800 rounded-lg p-8 w-full max-w-md">
          <h2 id="modalTitle" class="text-2xl font-semibold mb-4">Create New List</h2>
          <input v-model="newListTitle" type="text" placeholder="Enter list title" class="w-full px-4 py-2 rounded-md bg-gray-700 text-white mb-4">
          <div class="flex justify-end">
            <button @click="showNewListModal = false" class="text-gray-400 hover:text-gray-300 mr-4">Cancel</button>
            <button @click="createNewList" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-md">Create</button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import { UserIcon, PlusIcon, MapIcon, EyeIcon, ShareIcon } from 'lucide-vue-next'
  
  const lists = ref([
    { id: 1, title: 'Favorite Restaurants', placesCount: 5 },
    { id: 2, title: 'Travel Wishlist', placesCount: 10 },
    { id: 3, title: 'Best Cafes', placesCount: 3 },
  ])
  
  const showNewListModal = ref(false)
  const newListTitle = ref('')
  
  const createNewList = () => {
    if (newListTitle.value.trim()) {
      const newList = {
        id: Date.now(),
        title: newListTitle.value.trim(),
        placesCount: 0
      }
      lists.value.push(newList)
      newListTitle.value = ''
      showNewListModal.value = false
    }
  }
  </script>