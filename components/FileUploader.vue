<script setup>
const emit = defineEmits(['files-selected'])

const handleFiles = async (event) => {
  const fileList = event.target.files
  if (!fileList?.length) return

  const files = await Promise.all(
    Array.from(fileList).map((file) => {
      return new Promise((resolve) => {
        const reader = new FileReader()
        reader.onload = () => resolve({ file, preview: reader.result })
        reader.readAsDataURL(file)
      })
    })
  )

  emit('files-selected', files)
}
</script>

<template>
  <div class="p-6 border-2 border-dashed border-gray-400 rounded-xl text-center bg-white shadow">
    <p class="text-gray-600 mb-2">📁 Click to upload files</p>
    <input type="file" multiple @change="handleFiles" />
  </div>
</template>
