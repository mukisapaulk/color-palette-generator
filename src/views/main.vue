<template>
  <div class="flex flex-col min-h-screen max-h-screen bg-beige-100 overflow-hidden font-mono">
    <!-- Header -->
    <header class="flex justify-between items-center px-6 py-3 bg-beige-200 border-b border-pixelated">
      <h1 class="text-xl font-bold text-gray-900 tracking-wider pixelated-text">
        Color Pall
      </h1>
      <div class="hidden md:flex items-center space-x-4">
        <select
          class="border border-gray-300 rounded-lg px-3 py-1 text-sm text-gray-700 bg-white hover:border-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-500"
          aria-label="Color palette tools"
        >
          <option>Tools</option>
          <option disabled>More tools (coming soon)</option>
        </select>
      </div>
    </header>

    <!-- Main Content -->
    <div class="flex-1 flex flex-col items-center justify-center px-6 py-4 space-y-4">
      <!-- Centered Instruction Text -->
      <div class="flex items-center justify-center h-full">
        <p class="text-center text-base font-medium text-gray-600 mb-4 max-w-md">
          Generate a color palette for web design or graphic projects using the spacebar or button below.
        </p>
      </div>

      <!-- Toolbar -->
      <div class="flex justify-center space-x-3 opacity-75 hover:opacity-100 transition-opacity">
        <button
          class="p-2 hover:bg-gray-100 rounded-lg transition-all hover:scale-105 flex flex-col items-center"
          title="Camera (Image Extraction)"
          @click="handleCamera"
          aria-label="Extract colors from image"
        >
          <svg
            class="w-4 h-4 mb-1"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
            alt="Camera icon for color extraction"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z"
            ></path>
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 13a3 3 0 11-6 0 3 3 0 016 0z"
            ></path>
          </svg>
          <span class="text-xs font-medium text-gray-600">Camera</span>
        </button>

        <button
          class="p-2 hover:bg-gray-100 rounded-lg transition-all hover:scale-105 flex flex-col items-center"
          title="Toggle Grid View"
          @click="toggleGridView"
          aria-label="Toggle grid view for color palette"
        >
          <svg
            class="w-4 h-4 mb-1"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
            alt="Grid icon for toggling view"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"
            ></path>
          </svg>
          <span class="text-xs font-medium text-gray-600">
            {{ isGridView ? 'List' : 'Grid' }}
          </span>
        </button>

        <button
          class="p-2 hover:bg-gray-100 rounded-lg transition-all hover:scale-105 flex flex-col items-center"
          title="Adjust Colors"
          @click="adjustColors"
          aria-label="Adjust color palette hues"
        >
          <svg
            class="w-4 h-4 mb-1"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
            alt="Adjust icon for color tweaking"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"
            ></path>
          </svg>
          <span class="text-xs font-medium text-gray-600">Adjust</span>
        </button>

        <button
          class="p-2 hover:bg-gray-100 rounded-lg transition-all hover:scale-105 flex flex-col items-center"
          title="Export Palette"
          @click="exportPalette"
          aria-label="Export color palette as JSON"
        >
          <svg
            class="w-4 h-4 mb-1"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
            alt="Export icon for downloading palette"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"
            ></path>
          </svg>
          <span class="text-xs font-medium text-gray-600">Export</span>
        </button>

        <button
          class="p-2 hover:bg-gray-100 rounded-lg transition-all hover:scale-105 flex flex-col items-center"
          title="Save Palette"
          @click="savePalette"
          aria-label="Save color palette to local storage"
        >
          <svg
            class="w-4 h-4 mb-1"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
            alt="Save icon for storing palette"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
            ></path>
          </svg>
          <span class="text-xs font-medium text-gray-600">Save</span>
        </button>
      </div>

      <!-- Palette Section -->
      <div class="w-full h-[50vh] lg:h-[55vh]">
        <Palette
          :colors="colors"
          :is-grid-view="isGridView"
          @update-color="updateColor"
          @show-modal="showModal"
        />
      </div>
    </div>

    <!-- Floating Action Button -->
    <div class="group fixed bottom-6 right-6">
      <button
        class="bg-blue-500 text-white p-4 rounded-full shadow-lg hover:bg-blue-600 transition-all hover:scale-110 focus:outline-none focus:ring-2 focus:ring-blue-300"
        title="Generate New Palette"
        aria-label="Generate new color palette for design"
        @click="handleGenerate"
      >
        <svg
          class="w-6 h-6"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
          alt="Generate icon for new color palette"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"
          ></path>
        </svg>
      </button>
      <span
        class="absolute right-0 bottom-14 px-2 py-1 bg-gray-800 text-white text-xs rounded opacity-0 group-hover:opacity-100 transition-opacity"
      >
        Generate Palette
      </span>
    </div>

    <!-- Modal for Feedback -->
    <Modal :is-open="modal.isOpen" :message="modal.message" @close="closeModal" />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import axios from 'axios'
import Palette from '@/components/Palette.vue'
import Modal from '@/components/Modal.vue'

defineOptions({ name: 'MainView' })

const colors = ref([])
const isGridView = ref(false)
const modal = ref({ isOpen: false, message: '' })
let isGenerating = false

async function generatePalette() {
  const newColors = Array.from({ length: 5 }, () => ({
    hex: `#${Math.floor(Math.random() * 16777215)
      .toString(16)
      .padStart(6, '0')}`,
    name: 'Unknown',
  }))

  const requests = newColors.map((color) =>
    axios
      .get(`https://www.thecolorapi.com/id?hex=${color.hex.slice(1)}`)
      .then((res) => res.data.name.value || 'Unknown')
      .catch(() => 'Unknown')
  )

  const names = await Promise.all(requests)
  newColors.forEach((color, i) => (color.name = names[i]))
  return newColors
}

function showModal(message) {
  modal.value = { isOpen: true, message }
}

function closeModal() {
  modal.value.isOpen = false
}

function handleCamera() {
  showModal('Image-based color extraction coming soon!')
}

function toggleGridView() {
  isGridView.value = !isGridView.value
}

async function adjustColors() {
  const newColors = colors.value.map((color) => {
    const hsl = hexToHSL(color.hex)
    hsl.h = (hsl.h + (Math.random() * 40 - 20)) % 360
    return { hex: hslToHex(hsl.h, hsl.s, hsl.l), name: 'Unknown' }
  })

  const requests = newColors.map((color) =>
    axios
      .get(`https://www.thecolorapi.com/id?hex=${color.hex.slice(1)}`)
      .then((res) => res.data.name.value || 'Unknown')
      .catch(() => 'Unknown')
  )

  const names = await Promise.all(requests)
  newColors.forEach((color, i) => (color.name = names[i]))
  colors.value = newColors
}

function exportPalette() {
  const blob = new Blob([JSON.stringify(colors.value, null, 2)], {
    type: 'application/json',
  })
  const url = URL.createObjectURL(blob)
  const link = document.createElement('a')
  link.href = url
  link.download = 'palette.json'
  link.click()
  URL.revokeObjectURL(url)
  showModal('Palette exported as JSON!')
}

function savePalette() {
  localStorage.setItem('savedPalette', JSON.stringify(colors.value))
  showModal('Palette saved successfully!')
}

async function updateColor({ index, newHex }) {
  const color = colors.value[index]
  color.hex = newHex
  try {
    const res = await axios.get(`https://www.thecolorapi.com/id?hex=${newHex.slice(1)}`)
    color.name = res.data.name.value || 'Unknown'
  } catch {
    color.name = 'Unknown'
    showModal('Error fetching color name.')
  }
  colors.value = [...colors.value]
}

async function handleGenerate() {
  if (!isGenerating) {
    isGenerating = true
    colors.value = await generatePalette()
    setTimeout(() => (isGenerating = false), 300)
  }
}

function handleKeydown(e) {
  if (e.code === 'Space' && !isGenerating) {
    e.preventDefault()
    isGenerating = true
    generatePalette()
      .then((newColors) => (colors.value = newColors))
      .finally(() => setTimeout(() => (isGenerating = false), 300))
  }
}

function hexToHSL(hex) {
  let r = parseInt(hex.slice(1, 3), 16) / 255
  let g = parseInt(hex.slice(3, 5), 16) / 255
  let b = parseInt(hex.slice(5, 7), 16) / 255
  const max = Math.max(r, g, b),
    min = Math.min(r, g, b)
  let h,
    s,
    l = (max + min) / 2
  if (max === min) {
    h = s = 0
  } else {
    const d = max - min
    s = l > 0.5 ? d / (2 - max - min) : d / (max + min)
    switch (max) {
      case r:
        h = (g - b) / d + (g < b ? 6 : 0)
        break
      case g:
        h = (b - r) / d + 2
        break
      case b:
        h = (r - g) / d + 4
        break
    }
    h /= 6
  }
  return { h: h * 360, s: s * 100, l: l * 100 }
}

function hslToHex(h, s, l) {
  l /= 100
  const a = (s * Math.min(l, 1 - l)) / 100
  const f = (n) => {
    const k = (n + h / 30) % 12
    const c = l - a * Math.max(Math.min(k - 3, 9 - k, 1), -1)
    return Math.round(255 * c)
      .toString(16)
      .padStart(2, '0')
  }
  return `#${f(0)}${f(8)}${f(4)}`
}

onMounted(async () => {
  colors.value = await generatePalette()
  window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
</script>

<style scoped>
* {
  transition: all 0.2s ease-in-out;
}

.bg-beige-100 {
  background-color: #f5f5dc;
}
.bg-beige-200 {
  background-color: #e0d8c0;
}
.border-pixelated {
  border-bottom: 2px dashed #808080;
}
.pixelated-text {
  font-family: 'Courier New', monospace;
  text-shadow: 1px 1px #000;
}
</style>
