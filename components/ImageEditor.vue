<script setup>
import { ref, onMounted, watch } from 'vue'
import Cropper from 'cropperjs'
import 'cropperjs/dist/cropper.css'

const props = defineProps({
  file: Object,        // File to edit
  visible: Boolean     // Controls modal visibility
})
const emit = defineEmits(['close', 'save'])

const imagePreview = ref(null)
const cropper = ref(null)
const newName = ref(props.file?.name || '')

watch(() => props.visible, (val) => {
  if (val) newName.value = props.file?.name || ''
})

onMounted(() => {
  watch(imagePreview, (el) => {
    if (el && props.file) {
      const url = URL.createObjectURL(props.file)
      el.src = url
      cropper.value = new Cropper(el, {
        viewMode: 1,
        aspectRatio: NaN,
        autoCropArea: 1,
        responsive: true,
      })
    }
  })
})

const rotate = () => {
  cropper.value?.rotate(90)
}

const saveCropped = () => {
  const canvas = cropper.value?.getCroppedCanvas()
  canvas.toBlob((blob) => {
    const editedFile = new File([blob], newName.value || props.file.name, {
      type: props.file.type,
    })
    emit('save', editedFile)
    emit('close')
  }, props.file.type)
}
</script>

<template>
  <div v-if="visible" class="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center z-50">
    <div class="bg-white p-4 rounded-xl w-[90vw] max-w-2xl space-y-4">
      <h2 class="text-lg font-semibold text-center">Edit Image</h2>

      <!-- Rename -->
      <input
        v-model="newName"
        class="w-full p-2 border rounded text-sm"
        placeholder="Rename file"
      />

      <!-- Image Cropper -->
      <div class="max-h-[400px] overflow-auto border rounded">
        <img ref="imagePreview" class="max-w-full max-h-[400px]" />
      </div>

      <!-- Actions -->
      <div class="flex justify-between items-center">
        <button @click="rotate" class="bg-blue-500 text-white px-3 py-1 rounded hover:bg-blue-600">
          🔄 Rotate
        </button>
        <div class="space-x-2">
          <button @click="$emit('close')" class="bg-gray-400 text-white px-3 py-1 rounded hover:bg-gray-500">
            Cancel
          </button>
          <button @click="saveCropped" class="bg-green-500 text-white px-3 py-1 rounded hover:bg-green-600">
            ✅ Save & Upload
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* CropperJS styling (already imported) */
</style>
