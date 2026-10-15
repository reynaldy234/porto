<script setup lang="ts">
import { ArrowUp } from 'lucide-vue-next'

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="py-12 border-t border-white/[0.08] bg-[#040507] relative z-10">
    <div class="site-container flex flex-col md:flex-row items-center justify-between gap-6">
      
      <!-- Left Info -->
      <div class="flex flex-col items-center md:items-start text-center md:text-left">
        <div class="flex items-center gap-2">
          <span class="font-brand text-white font-bold text-sm tracking-wide">
            REYNALDY IRSYAD
          </span>
          <span class="text-slate-500 font-mono text-xs">/</span>
          <span class="text-xs font-mono text-sky-400">TELKOM UNIVERSITY</span>
        </div>
        <p class="text-slate-500 text-xs mt-1 font-mono">
          System Analyst &bull; Business Analyst &bull; Web Development
        </p>
      </div>

      <!-- Quick Nav Links -->
      <div class="flex items-center gap-6 text-xs font-mono text-slate-400">
        <a href="#about" class="hover:text-white transition-colors">Tentang</a>
        <a href="#skills" class="hover:text-white transition-colors">Keahlian</a>
        <a href="#projects" class="hover:text-white transition-colors">Projek</a>
        <a href="#certificate" class="hover:text-white transition-colors">Sertifikat</a>
        <a href="#contact" class="hover:text-white transition-colors">Kontak</a>
      </div>

      <!-- Back to Top Button -->
      <div>
        <button
          @click="scrollToTop"
          class="flex items-center gap-2 px-3.5 py-2 rounded-full bg-white/[0.04] border border-white/[0.08] text-xs font-mono text-slate-300 hover:text-white hover:bg-white/[0.08] transition-all"
        >
          <span>Kembali ke Atas</span>
          <ArrowUp class="w-3.5 h-3.5 text-sky-400" />
        </button>
      </div>

    </div>

    <!-- Bottom Copyright -->
    <div class="site-container mt-8 pt-6 border-t border-white/[0.04] flex flex-col sm:flex-row items-center justify-between text-[11px] font-mono text-slate-400 gap-2">
      <div>
        &copy; 2026 Reynaldy Irsyad. All rights reserved.
      </div>
      <div>
        Built with Vue 3 &bull; Motion &bull; Modern Design System
      </div>
    </div>
  </footer>
</template>
