<script setup lang="ts">
const items = [
  'SYSTEM ANALYSIS',
  'BUSINESS ANALYSIS',
  'WEB DEVELOPMENT',
  'DATA WAREHOUSE & DWBI',
  'AGILE SCRUM METHODOLOGY',
  'BPMN PROCESS MAPPING',
  'TELKOM UNIVERSITY',
  'SIKAPTUJ SYSTEM',
  'LAPORKOTA PLATFORM',
  'KPI & SALES DASHBOARD',
  'REQUIREMENTS ENGINEERING',
  'VUE.JS & TYPESCRIPT',
]
</script>

<template>
  <div class="site-container my-8">
    <div class="relative py-3.5 px-2 rounded-2xl border border-white/[0.08] bg-[#0c0f17]/70 overflow-hidden backdrop-blur-md shadow-xl shadow-black/30">
      <!-- Gradient Fade Masks at edges (matching capsule background) -->
      <div class="absolute left-0 top-0 bottom-0 w-16 sm:w-24 bg-gradient-to-r from-[#0c0f17] to-transparent z-10 pointer-events-none"></div>
      <div class="absolute right-0 top-0 bottom-0 w-16 sm:w-24 bg-gradient-to-l from-[#0c0f17] to-transparent z-10 pointer-events-none"></div>

      <div class="marquee-track flex items-center">
        <!-- First copy -->
        <div class="flex items-center gap-8 shrink-0 pr-8">
          <template v-for="(item, idx) in items" :key="`a-${idx}`">
            <span class="font-display font-bold text-xs sm:text-sm tracking-widest text-slate-400/90 uppercase flex items-center gap-8">
              <span>{{ item }}</span>
              <span class="w-1.5 h-1.5 rounded-full bg-sky-400/60 shadow-[0_0_8px_rgba(56,189,248,0.8)]"></span>
            </span>
          </template>
        </div>

        <!-- Second copy for seamless continuous loop -->
        <div class="flex items-center gap-8 shrink-0 pr-8" aria-hidden="true">
          <template v-for="(item, idx) in items" :key="`b-${idx}`">
            <span class="font-display font-bold text-xs sm:text-sm tracking-widest text-slate-400/90 uppercase flex items-center gap-8">
              <span>{{ item }}</span>
              <span class="w-1.5 h-1.5 rounded-full bg-sky-400/60 shadow-[0_0_8px_rgba(56,189,248,0.8)]"></span>
            </span>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>
