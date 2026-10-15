<script setup lang="ts">
import { ref } from 'vue'
import {
  Layers,
  TrendingUp,
  BarChart3,
  Code2,
  CheckCircle2
} from 'lucide-vue-next'

const activeCategory = ref('all')

const categories = [
  { id: 'all', label: 'Semua Bidang' },
  { id: 'sa', label: 'System Analysis' },
  { id: 'ba', label: 'Business Analysis' },
  { id: 'dwbi', label: 'Data & BI' },
  { id: 'dev', label: 'Web & Agile' },
]

const competencies = [
  {
    category: 'sa',
    title: 'System Analysis & Specification',
    icon: Layers,
    badge: 'CORE EXPERTISE',
    color: 'from-sky-500/20 to-blue-600/20',
    borderColor: 'border-sky-500/30',
    textColor: 'text-sky-400',
    desc: 'Menganalisis arsitektur sistem, kebutuhan fungsional & non-fungsional, serta merancang alur sistem terpadu seperti pada sistem SIKAPTUJ Telkom University.',
    skills: [
      'BPMN 2.0 Process Mapping',
      'Software Requirements Specification (SRS)',
      'Use Case & Activity Diagrams',
      'Entity Relationship (ERD) & Data Modeling',
      'Master Data Architecture'
    ]
  },
  {
    category: 'ba',
    title: 'Business Analysis & Process Engineering',
    icon: TrendingUp,
    badge: 'STRATEGY',
    color: 'from-indigo-500/20 to-purple-600/20',
    borderColor: 'border-indigo-500/30',
    textColor: 'text-indigo-400',
    desc: 'Menjembatani kebutuhan bisnis stakeholder dengan solusi teknis melalui pendekatan analitis, pemetaan proses bisnis, dan optimalisasi alur kerja organisasi.',
    skills: [
      'Business Process Re-engineering',
      'Stakeholder Interviews & Alignment',
      'Gap Analysis & Feasibility Study',
      'Cost-Benefit & Operational Impact',
      'User Acceptance Testing (UAT)'
    ]
  },
  {
    category: 'dwbi',
    title: 'Data Warehouse & Business Intelligence',
    icon: BarChart3,
    badge: 'ANALYTICS',
    color: 'from-amber-500/20 to-orange-600/20',
    borderColor: 'border-amber-500/30',
    textColor: 'text-amber-400',
    desc: 'Mengolah dataset skala besar menjadi insight strategis dan dashboard interaktif untuk evaluasi kinerja operasional dan perhitungan KPI penjualan.',
    skills: [
      'Sales KPI & Performance Tracking',
      'E-Commerce Data Analysis (Amazon 2022)',
      'Order Cancellation & Success Analysis',
      'Data Modeling & Dimensional Schemas',
      'Executive BI Dashboarding'
    ]
  },
  {
    category: 'dev',
    title: 'Web Development & Agile Scrum',
    icon: Code2,
    badge: 'IMPLEMENTATION',
    color: 'from-emerald-500/20 to-teal-600/20',
    borderColor: 'border-emerald-500/30',
    textColor: 'text-emerald-400',
    desc: 'Membangun aplikasi website modern dan interaktif dengan kolaborasi tim berbasis metode Agile Scrum untuk penyelesaian masalah nyata (LaporKota & SIKAPTUJ).',
    skills: [
      'Vue.js & TypeScript',
      'Full-Stack Web Architecture',
      'Agile Scrum Framework & Sprints',
      'RESTful API Design & Integration',
      'Git Version Control & Collaboration'
    ]
  }
]
</script>

<template>
  <section id="skills" class="py-24 relative">
    <div class="site-container relative z-10">
      
      <!-- Section Header -->
      <div class="mb-10">
        <div>
          <div class="flex items-center gap-2 mb-3">
            <span class="w-8 h-[2px] bg-sky-400"></span>
            <span class="font-mono text-xs uppercase tracking-wider text-sky-400 font-semibold">
              01 // CORE COMPETENCIES
            </span>
          </div>
          <h2 class="font-display font-black text-3xl sm:text-4xl md:text-5xl text-white uppercase tracking-tight">
            KEAHLIAN &amp; <span class="text-gradient-cyan">KOMPETENSI</span>
          </h2>
        </div>
      </div>

      <!-- Category Filter Pills -->
      <div class="flex flex-wrap gap-2 mb-10">
        <button
          v-for="cat in categories"
          :key="cat.id"
          @click="activeCategory = cat.id"
          class="px-4 py-2 rounded-full text-xs font-mono font-medium transition-all duration-200 outline-none border-0 cursor-pointer"
          :class="activeCategory === cat.id ? 'bg-sky-500 text-slate-950 font-bold shadow-lg shadow-sky-500/30' : 'bg-white/[0.05] text-slate-400 hover:bg-white/[0.09] hover:text-slate-200'"
        >
          {{ cat.label }}
        </button>
      </div>

      <!-- Competency Cards Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <template v-for="(comp, index) in competencies" :key="index">
          <div
            v-if="activeCategory === 'all' || activeCategory === comp.category"
            class="glass-panel p-6 sm:p-8 rounded-2xl relative overflow-hidden group hover:border-white/[0.22] transition-all duration-300 flex flex-col justify-between"
          >
            <!-- Ambient Card Glow on Hover -->
            <div
              class="absolute -right-16 -top-16 w-48 h-48 rounded-full bg-gradient-to-br opacity-0 group-hover:opacity-100 transition-opacity duration-500 blur-2xl pointer-events-none"
              :class="comp.color"
            ></div>

            <div>
              <!-- Top Row: Icon & Badge -->
              <div class="flex items-center justify-between mb-6">
                <div
                  class="w-12 h-12 rounded-xl flex items-center justify-center border bg-white/[0.03]"
                  :class="[comp.borderColor, comp.textColor]"
                >
                  <component :is="comp.icon" class="w-6 h-6" />
                </div>

                <span
                  class="font-mono text-[10px] font-bold px-3 py-1 rounded-full border bg-white/[0.02]"
                  :class="[comp.borderColor, comp.textColor]"
                >
                  {{ comp.badge }}
                </span>
              </div>

              <!-- Title & Description -->
              <h3 class="font-display font-bold text-xl text-white mb-3 group-hover:text-sky-300 transition-colors">
                {{ comp.title }}
              </h3>
              <p class="text-slate-400 text-xs sm:text-sm leading-relaxed mb-6 font-sans">
                {{ comp.desc }}
              </p>
            </div>

            <!-- Detailed Skills List -->
            <div class="pt-5 border-t border-white/[0.06]">
              <div class="font-mono text-[11px] text-slate-400 uppercase tracking-wider mb-3">
                Key Deliverables &amp; Focus
              </div>
              <ul class="space-y-2">
                <li
                  v-for="(skill, sIdx) in comp.skills"
                  :key="sIdx"
                  class="flex items-center gap-2.5 text-xs text-slate-300 font-sans"
                >
                  <CheckCircle2 class="w-3.5 h-3.5 shrink-0 text-sky-400/80" />
                  <span>{{ skill }}</span>
                </li>
              </ul>
            </div>

          </div>
        </template>
      </div>

    </div>
  </section>
</template>
