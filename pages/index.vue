<script setup>
import CalendarRange from '~/components/CalendarRange.vue'
import FileUploader from '~/components/FileUploader.vue'
import FilePreviewer from '~/components/FilePreviewer.vue'
import { ref } from 'vue'

const files = ref([])

const handleRangeUpdate = (range) => {
  console.log('📅 Selected Range:', range)
}

const handleFiles = (selected) => {
  console.log('✅ Uploaded Files:', selected)
  files.value = selected
}
</script>

<template>
  <div class="space-y-8">
    <CalendarRange @update:range="handleRangeUpdate" />

    <FileUploader @files-selected="handleFiles" />

    <FilePreviewer :files="files" />
  </div>
</template>
