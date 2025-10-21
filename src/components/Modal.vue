<template>
  <div v-if="isOpen" class="fixed inset-0 flex items-center justify-center bg-gray-800 bg-opacity-30 z-50 backdrop-blur-sm">
    <div class="bg-gradient-to-b from-beige-100 to-beige-200 border-4 border-double border-gray-600 rounded-sm shadow-xl max-w-sm w-full text-center animate-glitch">
      <!-- Retro Title Bar -->
      <div class="bg-blue-600 text-white px-2 py-1 text-sm font-mono border-b border-gray-600 flex justify-between items-center">
        <span>PaletteGen Alert!</span>
        <button class="text-white hover:text-gray-300" @click="$emit('close')" aria-label="Close modal">
          ✕
        </button>
      </div>
      <!-- Content -->
      <div class="p-6">
        <p class="text-gray-800 mb-4 text-sm font-mono pixelated-text">{{ message }}</p>
        <button
          class="bg-blue-300 text-white px-4 py-2 border-2 border-gray-600 rounded-sm shadow-[3px_3px_0_#000] hover:shadow-[1px_1px_0_#000] hover:translate-x-0.5 hover:translate-y-0.5 hover:scale-105 transition-all"
          @click="$emit('close')"
          aria-label="Close color palette alert"
        >
          OK
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineOptions({ name: 'PaletteModal' });

defineProps({
  isOpen: { type: Boolean, default: false },
  message: { type: String, default: '' },
});
</script>

<style scoped>
.bg-beige-100 { background-color: #f5f5dc; }
.bg-beige-200 { background-color: #e0d8c0; }
.bg-blue-300 { background-color: #4DB8E6; }
.bg-blue-600 { background-color: #2A4B7C; }
.pixelated-text { font-family: 'Courier New', monospace; text-shadow: 1px 1px #000; }

.backdrop-blur-sm { backdrop-filter: blur(2px); }

@keyframes glitch {
  0% { transform: translate(0); }
  20% { transform: translate(-2px, 1px); }
  40% { transform: translate(2px, -1px); }
  60% { transform: translate(-1px, 0); }
  100% { transform: translate(0); }
}

.animate-glitch {
  animation: glitch 0.3s ease-in-out;
}
</style>
