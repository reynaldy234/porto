<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue'
import { X, ExternalLink } from 'lucide-vue-next'

const props = defineProps<{
  isOpen: boolean
  title: string
  image: string
  caption?: string
}>()

const emit = defineEmits<{
  (e: 'close'): void
}>()

const handleKeydown = (e: KeyboardEvent) => {
  if (e.key === 'Escape' && props.isOpen) {
    emit('close')
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
</script>

<template>
  <transition
    enter-active-class="transition duration-200 ease-out"
    enter-from-class="opacity-0"
    enter-to-class="opacity-100"
    leave-active-class="transition duration-150 ease-in"
    leave-from-class="opacity-100"
    leave-to-class="opacity-0"
  >
    <div
      v-if="isOpen"
      class="fixed inset-0 z-50 flex items-center justify-center p-4 sm:p-6 bg-black/85 backdrop-blur-md"
      @click.self="emit('close')"
    >
      <div class="relative max-w-5xl w-full bg-[#0d1017] rounded-2xl border border-white/[0.15] shadow-2xl overflow-hidden flex flex-col max-h-[92vh]">
        
        <!-- Header -->
        <div class="flex items-center justify-between px-5 py-3.5 border-b border-white/[0.08] bg-[#121622]">
          <div>
            <h4 class="font-display font-bold text-white text-sm sm:text-base">
              {{ title }}
            </h4>
            <p v-if="caption" class="text-xs font-mono text-slate-400 mt-0.5">
              {{ caption }}
            </p>
          </div>

          <div class="flex items-center gap-2">
            <a
              :href="image"
              target="_blank"
              class="p-2 rounded-lg bg-white/[0.05] hover:bg-white/[0.1] text-slate-300 hover:text-white transition-colors"
              title="Buka Tab Baru"
            >
              <ExternalLink class="w-4 h-4" />
            </a>
            <button
              @click="emit('close')"
              class="p-2 rounded-lg bg-white/[0.05] hover:bg-white/[0.1] text-slate-300 hover:text-white transition-colors"
              title="Tutup (Esc)"
            >
              <X class="w-5 h-5" />
            </button>
          </div>
        </div>

        <!-- Body Image -->
        <div class="p-2 sm:p-4 overflow-auto flex items-center justify-center bg-[#07090e]">
          <img
            :src="image"
            :alt="title"
            class="max-w-full max-h-[76vh] object-contain rounded-lg shadow-xl"
          />
        </div>

      </div>
    </div>
  </transition>
</template>
