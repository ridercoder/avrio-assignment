<script setup>
import { ref, watch } from 'vue'
import dayjs from 'dayjs'

const emit = defineEmits(['update:range'])

const startDate = ref(dayjs().subtract(7, 'day').format('YYYY-MM-DD'))
const endDate = ref(dayjs().format('YYYY-MM-DD'))
const tillNow = ref(false)

const goBack = () => {
  startDate.value = dayjs(startDate.value).subtract(7, 'day').format('YYYY-MM-DD')
  endDate.value = dayjs(endDate.value).subtract(7, 'day').format('YYYY-MM-DD')
}

const goForward = () => {
  startDate.value = dayjs(startDate.value).add(7, 'day').format('YYYY-MM-DD')
  endDate.value = dayjs(endDate.value).add(7, 'day').format('YYYY-MM-DD')
}

watch([startDate, endDate, tillNow], () => {
  emit('update:range', {
    start: startDate.value,
    end: tillNow.value ? 'Till Now' : endDate.value
  })
})
</script>

<template>
  <div class="flex flex-wrap items-center gap-4 bg-white shadow-md p-5 rounded-xl text-sm max-w-full">
    <!-- Back Arrow -->
    <button
      @click="goBack"
      class="text-gray-500 hover:text-blue-600 text-xl transition"
    >
      ◀️
    </button>

    <!-- Date Inputs -->
    <div class="flex items-center gap-2">
      <input
        type="date"
        v-model="startDate"
        class="border px-3 py-2 rounded-md focus:ring-2 focus:ring-blue-400 outline-none text-sm"
      />
      <span>to</span>
      <input
        type="date"
        v-model="endDate"
        :disabled="tillNow"
        class="border px-3 py-2 rounded-md focus:ring-2 focus:ring-blue-400 outline-none text-sm disabled:opacity-50"
      />
    </div>

    <!-- Till Now -->
    <label class="flex items-center gap-2 text-gray-700 cursor-pointer select-none">
      <input
        type="checkbox"
        v-model="tillNow"
        class="accent-blue-600 w-4 h-4"
      />
      Till Now
    </label>

    <!-- Forward Arrow -->
    <button
      @click="goForward"
      class="text-gray-500 hover:text-blue-600 text-xl transition"
    >
      ▶️
    </button>
  </div>
</template>
