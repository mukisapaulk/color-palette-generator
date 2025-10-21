<template>
  <div :class="isGridView ? 'grid grid-cols-2 lg:grid-cols-3 gap-2 h-full' : 'flex flex-col lg:flex-row h-full gap-2'">
    <div
      v-for="(color, index) in colors"
      :key="index"
      class="flex-1 relative rounded-lg overflow-hidden shadow-lg hover:shadow-xl transition-all duration-300 hover:scale-[1.02] pixelated retro-scanlines"
      :style="{ background: `linear-gradient(135deg, ${color.hex} 0%, ${adjustBrightness(color.hex, 10)} 100%)`, minHeight: isGridView ? '100%' : '100px' }"
      tabindex="0"
      :aria-label="`Color ${color.hex.toUpperCase()}: ${color.name} for palette generator`"
    >
      <!-- Overlay Icons -->
      <div class="absolute top-2 right-2 flex space-x-1 opacity-0 hover:opacity-100 transition-opacity">
        <button
          class="bg-white/20 backdrop-blur-sm text-white px-2 py-1 rounded text-xs font-medium hover:bg-white/30"
          title="Lock color"
          aria-label="Lock color in palette"
        >
          Lock
        </button>
        <button
          class="bg-white/20 backdrop-blur-sm text-white px-2 py-1 rounded text-xs font-medium hover:bg-white/30"
          title="Adjust color"
          aria-label="Edit hex color in palette"
          @click="openEditModal(index)"
        >
          Edit
        </button>
      </div>

      <!-- Color Info -->
      <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black/60 to-transparent p-3 text-white">
        <div class="text-center">
          <p class="font-mono text-xs tracking-wide">{{ color.hex.toUpperCase() }}</p>
          <p class="text-[10px] font-light mt-1">{{ color.name }}</p>
          <button
            class="mt-1 inline-block bg-white/90 text-gray-900 text-[10px] px-2 py-1 rounded-full font-medium hover:bg-white transition-colors"
            @click="copyToClipboard(color.hex)"
            aria-label="Copy hex code for color palette"
          >
            Copy
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- Edit Modal -->
  <div v-if="editModal.isOpen" class="fixed inset-0 flex items-center justify-center bg-gray-800 bg-opacity-30 z-50 backdrop-blur-sm">
    <div class="bg-gradient-to-b from-beige-100 to-beige-200 border-4 border-double border-gray-600 rounded-sm shadow-xl max-w-sm w-full text-center animate-glitch">
      <!-- Retro Title Bar -->
      <div class="bg-blue-600 text-white px-2 py-1 text-sm font-mono border-b border-gray-600 flex justify-between items-center">
        <span>Edit Color</span>
        <button class="text-white hover:text-gray-300" @click="closeEditModal" aria-label="Close edit color modal">
          ✕
        </button>
      </div>
      <!-- Content -->
      <div class="p-6">
        <p class="text-gray-800 mb-4 text-sm font-mono pixelated-text">Enter new HEX code for your color palette:</p>
        <input v-model="newHex" type="text" class="border-2 border-gray-600 p-2 mb-4 w-full bg-beige-100 text-gray-800 font-mono text-sm" placeholder="#RRGGBB" aria-label="Input hex code for color palette" />
        <div class="flex justify-center space-x-4">
          <button
            class="bg-blue-300 text-white px-4 py-2 border-2 border-gray-600 rounded-sm shadow-[3px_3px_0_#000] hover:shadow-[1px_1px_0_#000] hover:translate-x-0.5 hover:translate-y-0.5 hover:scale-105 transition-all"
            @click="submitEdit"
            aria-label="Submit new hex code"
          >
            Submit
          </button>
          <button
            class="bg-gray-300 text-gray-800 px-4 py-2 border-2 border-gray-600 rounded-sm shadow-[3px_3px_0_#000] hover:shadow-[1px_1px_0_#000] hover:translate-x-0.5 hover:translate-y-0.5 hover:scale-105 transition-all"
            @click="closeEditModal"
            aria-label="Cancel edit"
          >
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineOptions({
  name: 'ColorPalette'
});
import { ref } from 'vue';

const props = defineProps({
  colors: { type: Array, required: true, default: () => [] },
  isGridView: { type: Boolean, default: false },
});

const emit = defineEmits(['update-color', 'show-modal']);

const editModal = ref({ isOpen: false, index: null });
const newHex = ref('');

function openEditModal(index) {
  editModal.value = { isOpen: true, index };
  newHex.value = props.colors[index].hex;
}

function closeEditModal() {
  editModal.value.isOpen = false;
}

function submitEdit() {
  if (/^#[0-9A-Fa-f]{6}$/.test(newHex.value)) {
    emit('update-color', { index: editModal.value.index, newHex: newHex.value });
    closeEditModal();
  } else {
    emit('show-modal', 'Invalid HEX code. Please use #RRGGBB format.');
  }
}

async function copyToClipboard(hex) {
  try {
    await navigator.clipboard.writeText(hex);
    emit('show-modal', 'HEX code copied to clipboard!');
  } catch (err) {
    console.error(err);
    emit('show-modal', 'Failed to copy HEX code.');
  }
}

function adjustBrightness(hex, percent) {
  const num = parseInt(hex.replace('#', ''), 16);
  const amt = Math.round(2.55 * percent);
  const R = (num >> 16) + amt;
  const G = (num >> 8 & 0x00FF) + amt;
  const B = (num & 0x0000FF) + amt;
  return '#' + (0x1000000 + (R < 255 ? R < 1 ? 0 : R : 255) * 0x10000 +
    (G < 255 ? G < 1 ? 0 : G : 255) * 0x100 +
    (B < 255 ? B < 1 ? 0 : B : 255)).toString(16).slice(1);
}
</script>

<style scoped>
.text-white {
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.3);
}

button:focus {
  outline: 2px solid #3B82F6;
  outline-offset: 2px;
}

.pixelated {
  image-rendering: pixelated;
}

.retro-scanlines {
  position: relative;
}

.retro-scanlines::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(0deg, rgba(0,0,0,0.05) 0px, rgba(0,0,0,0.05) 1px, transparent 1px, transparent 2px);
  pointer-events: none;
}

.bg-beige-100 { background-color: #f5f5dc; }
.bg-beige-200 { background-color: #e0d8c0; }
.bg-blue-300 { background-color: #4DB8E6; }
.bg-blue-600 { background-color: #2A4B7C; }
.pixelated-text { font-family: 'Courier New', monospace; text-shadow: 1px 1px #000; }

@keyframes glitch {
  0% { transform: translate(0); }
  20% { transform: translate(-2px, 1px); }
  40% { transform: translate(2px, -1px); }
  60% { transform: translate(-1px, 0); }
  100% { transform: translate(0); }
}
</style>
