<script setup>
defineProps({
  files: {
    type: Array,
    default: () => []
  }
})
</script>

<template>
  <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4 mt-4">
    <div
      v-for="(item, index) in files"
      :key="index"
      class="border rounded shadow bg-white p-3"
    >
      <div class="font-semibold text-gray-800 text-sm mb-2">
        📄 {{ item.file.name }}
      </div>
      <img
        v-if="item.file.type.startsWith('image/')"
        :src="item.preview"
        class="w-full h-32 object-cover rounded"
        alt="Preview"
      />
    </div>
  </div>
</template>
