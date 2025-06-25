<script setup>
import { ref } from 'vue'
import ImageEditor from './ImageEditor.vue'

const emit = defineEmits(['files-selected'])

const fileInput = ref(null)
const showEditor = ref(false)
const selectedFile = ref(null)
const uploadedFiles = ref([])

const handleFiles = (event) => {
  const fileList = event.target.files
  if (!fileList?.length) return

  // Open editor for the first file
  selectedFile.value = fileList[0]
  showEditor.value = true
}

// Called after editing is complete
const handleSave = (editedFile) => {
  const reader = new FileReader()
  reader.onload = () => {
    uploadedFiles.value.push({ file: editedFile, preview: reader.result })
    emit('files-selected', uploadedFiles.value)
  }
  reader.readAsDataURL(editedFile)
}
</script>

<template>
  <div class="w-full max-w-md p-6 border-2 border-dashed border-gray-400 rounded-xl text-center bg-white shadow hover:bg-gray-50 transition">
    <p class="text-gray-600 mb-2">📁 Click to upload an image</p>
    <input
      ref="fileInput"
      type="file"
      accept="image/*"
      class="cursor-pointer"
      @change="handleFiles"
    />

    <!-- Image Editor Modal -->
    <ImageEditor
      v-if="selectedFile"
      :visible="showEditor"
      :file="selectedFile"
      @close="showEditor = false"
      @save="handleSave"
    />
  </div>
</template>
