<script setup>
import { ref } from 'vue'

const props = defineProps({
  files: {
    type: Array,
    default: () => []
  }
})

const zoomImage = ref(null)
const showModal = ref(false)

const openZoom = (src) => {
  zoomImage.value = src
  showModal.value = true
}

const closeZoom = () => {
  showModal.value = false
  zoomImage.value = null
}
</script>

<template>
  <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4 mt-4">
    <div
      v-for="(item, index) in files"
      :key="index"
      class="border rounded shadow bg-white p-3 relative"
    >
      <!-- File name -->
      <div class="font-semibold text-gray-800 text-sm mb-2 truncate">
        📄 {{ item.file.name }}
      </div>

      <!-- Preview (zoomable) -->
      <img
        v-if="item.file.type.startsWith('image/')"
        :src="item.preview"
        class="w-full h-32 object-cover rounded cursor-zoom-in hover:opacity-80 transition"
        alt="Preview"
        @click="openZoom(item.preview)"
      />

      <!-- Download Button -->
      <a
        :href="item.preview"
        :download="item.file.name"
        class="absolute bottom-2 right-2 text-xs bg-blue-500 text-white px-2 py-1 rounded hover:bg-blue-600"
      >
        ⬇ Download
      </a>
    </div>
  </div>

  <!-- Zoom Modal -->
  <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-80 z-50 flex items-center justify-center">
    <div class="relative max-w-[90vw] max-h-[90vh]">
      <img :src="zoomImage" class="max-w-full max-h-full rounded-lg shadow-lg" />
      <button @click="closeZoom" class="absolute top-2 right-2 bg-red-500 text-white px-3 py-1 rounded hover:bg-red-600">
        ✖ Close
      </button>
    </div>
  </div>
</template>
