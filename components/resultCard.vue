<template>
  <div class="bg-white rounded-2xl shadow-md p-4 flex flex-col gap-2 w-full">
    <!-- Image + File Name -->
    <div>
      <img
        :src="imageUrl"
        alt="Result image"
        class="w-full h-64 object-contain rounded-md border border-green-950"
      />
      <a
        :href="imageUrl"
        target="_blank"
        class="text-blue-600 underline text-sm break-all"
      >
        {{ fileName }}
      </a>
    </div>

    <!-- Coordinates -->
    <div class="text-green-950 text-sm">
      <strong>Coordinates:</strong><br> {{ coordinates[0] }}, {{ coordinates[1] }}
    </div>

    <!-- Probability -->
    <div class="text-green-950 text-sm">
      <strong>Probability:</strong> {{ (probability * 100).toFixed(2) }}%
    </div>

    <!-- Feedback Buttons -->
    <div class="flex flex-row gap-2 mt-2">
      <button
        class="bg-green-100 text-green-800 px-4 py-1 rounded-full text-sm hover:bg-green-200"
        @click="sendFeedback(true)"
      >
        Has Condition
      </button>
      <button
        class="bg-red-100 text-red-800 px-4 py-1 rounded-full text-sm hover:bg-red-200"
        @click="sendFeedback(false)"
      >
        No Condition
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  imageUrl: String,
  probability: Number,
  fileName: String,
  coordinates: Array,
  onFeedback: Function
})

function sendFeedback(hasCondition) {
  if (typeof onFeedback === 'function') {
    onFeedback({ hasCondition })
  } else {
    console.log('Feedback:', hasCondition)
    // fallback logic (e.g., POST to API)
  }
}
</script>
