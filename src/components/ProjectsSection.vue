<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { Maximize2, Building2, ChevronLeft, ChevronRight } from 'lucide-vue-next'
import sikaptujImg from '../assets/sikaptuj.png'
import amazonImg from '../assets/amazon-dwbi.png'
import laporkotaImg from '../assets/laporkota.jpg'

const emit = defineEmits<{
  (e: 'open-modal', payload: { title: string; image: string; caption: string }): void
}>()

const projects = [
  {
    id: 'sikaptuj',
    tabLabel: 'SIKAPTUJ',
    shortType: 'Internship Web App',
    title: 'SIKAPTUJ — Sistem Manajemen Kerja Praktik',
    institution: 'Direktorat Kampus Jakarta Universitas Telkom',
    type: 'Internship (Kerja Praktik) Project',
    tagline: 'Aplikasi berbasis website untuk otomasi alur pendaftaran, pemantauan berkala, hingga rekapitulasi nilai KPPM mahasiswa.',
    image: sikaptujImg,
    period: 'Juli — September 2026',
    role: 'Full-Stack Developer & System Analyst Intern',
    description: 'Membuat aplikasi manajemen kerja praktek berbasis website (sikaptuj) untuk kelola progress kerja praktek hingga rekapitulasi nilai mahasiswa, sistem dosen untuk memantau perkembangan progress KP serta fitur admin untuk mengelola master data.',
    keyFeatures: [
      'Portal Mahasiswa: Pendaftaran KP/magang terstruktur, logbook berkala, dan pengunggahan hasil laporan akhir.',
      'Monitoring Dosen: Dashboard pemantauan perkembangan progress KP tiap mahasiswa bimbingan secara real-time.',
      'Sistem Admin: Pengelolaan master data akademik, penetapan dosen pembimbing, dan rekapitulasi nilai otomatis.'
    ],
    tags: ['Web Application', 'Telkom University', 'System Analysis', 'Master Data', 'Role-Based Access', 'Evaluation Management']
  },
  {
    id: 'amazon-dwbi',
    tabLabel: 'AMAZON DWBI',
    shortType: 'Data & BI Analytics',
    title: 'Amazon E-Commerce Sales & Financial KPI Dashboard',
    institution: 'Data Warehouse & Business Intelligence (DWBI)',
    type: 'Data & BI Analytics Project',
    tagline: 'Visualisasi analitis dan perhitungan KPI berbasis dataset Amazon 2022 dari Kaggle untuk evaluasi performa bisnis.',
    image: amazonImg,
    period: '2026 Academic Project',
    role: 'Business Intelligence & Data Analyst',
    description: 'Membuat dashboard business inteligence berdasarkan data Kaggle dengan dataset berjudul “Unlock Profits with E-Commerce Sales Data” yang berisi data transaksi penjualan Amazon pada tahun 2022. mencakup informasi penting seperti transaksi penjualan, produk, jumlah unit terjual, nilai penjualan, serta status pesanan dan pengiriman. Data utama ini digunakan sebagai dasar dalam mengevaluasi kinerja penjualan dan perhitungan KPI pada tahun 2022.',
    keyFeatures: [
      'Sales Performance Tracking: Analisis penjualan aktual $3.04M terhadap target penjualan $3.19M (+5.0% performa).',
      'Operational Metrics: Evaluasi mendalam Order Cancel Rate (12.18%) dan Delivery Success Rate (54.58%).',
      'Geographical & Category Breakdown: Pemetaan tingkat pembatalan per wilayah (Punjab, Jharkhand, Goa) dan kontribusi produk.'
    ],
    tags: ['Data Warehouse', 'Business Intelligence', 'Kaggle Dataset', 'KPI Calculation', 'Sales Analytics', 'Data Visualization']
  },
  {
    id: 'laporkota',
    tabLabel: 'LAPORKOTA',
    shortType: 'Agile Civic Tech',
    title: 'LaporKota — Sistem Manajemen Laporan Fasilitas Publik',
    institution: 'Projek Pengembangan Perangkat Lunak',
    type: 'Agile Scrum Collaborative Web Application',
    tagline: 'Sistem web terpadu untuk monitoring dan tindak lanjut laporan masyarakat atas infrastruktur kota yang bermasalah.',
    image: laporkotaImg,
    period: 'Collaborative Team Project',
    role: 'System Analyst & Scrum Collaborator',
    description: 'Sebuah projek berkelompok yang memanfaatkan metode agile scrum. LaporKota adalah sistem manajemen laporan kota berbasis web yang membantu admin dalam memonitor dan mengelola laporan masyarakat tentang berbagai masalah publik seperti jalan rusak, sampah menumpuk, lampu jalan mati, banjir, dan masalah fasilitas umum lainnya.',
    keyFeatures: [
      'Multi-Issue Tracking: Pelaporan publik untuk jalan rusak, sampah menumpuk, lampu jalan padam, dan risiko banjir.',
      'Admin Monitoring Center: Dashboard real-time untuk verifikasi kelayakan laporan dan penugasan tim perbaikan ke lapangan.',
      'Agile Scrum Workflow: Kolaborasi tim lintas sprint, backlog grooming, pemodelan user story, dan daily standup sync.'
    ],
    tags: ['Agile Scrum', 'Civic Tech', 'Issue Tracking', 'Problem Management', 'Web Application', 'Geo-Mapping']
  }
]

const currentIndex = ref(0)
const currentProj = computed(() => projects[currentIndex.value])

const nextProject = () => {
  currentIndex.value = (currentIndex.value + 1) % projects.length
}

const prevProject = () => {
  currentIndex.value = (currentIndex.value - 1 + projects.length) % projects.length
}

const selectProject = (index: number) => {
  currentIndex.value = index
}

const handlePreview = (proj: typeof projects[0]) => {
  emit('open-modal', {
    title: proj.title,
    image: proj.image,
    caption: `${proj.type} • ${proj.institution}`
  })
}

// Keyboard arrow navigation
const handleKeyDown = (e: KeyboardEvent) => {
  if (e.key === 'ArrowRight') nextProject()
  if (e.key === 'ArrowLeft') prevProject()
}

// Touch swipe navigation for mobile
let touchStartX = 0
let touchEndX = 0

const onTouchStart = (e: TouchEvent) => {
  touchStartX = e.changedTouches[0].screenX
}

const onTouchEnd = (e: TouchEvent) => {
  touchEndX = e.changedTouches[0].screenX
  if (touchStartX - touchEndX > 50) {
    nextProject()
  } else if (touchEndX - touchStartX > 50) {
    prevProject()
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeyDown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeyDown)
})
</script>

<template>
  <section id="projects" class="py-24 relative">
    <div class="site-container relative z-10">
      
      <!-- Section Header with generous bottom spacing -->
      <div class="mb-14">
        <div>
          <div class="flex items-center gap-2 mb-3">
            <span class="w-8 h-[2px] bg-sky-400"></span>
            <span class="font-mono text-xs uppercase tracking-wider text-sky-400 font-semibold">
              02 // PORTFOLIO &amp; EXPERIENCE
            </span>
          </div>
          <h2 class="font-display font-black text-3xl sm:text-4xl md:text-5xl text-white uppercase tracking-tight">
            PENGALAMAN &amp; <span class="text-gradient-cyan">PROJEK UTAMA</span>
          </h2>
        </div>
      </div>

      <!-- Slider Container with Left & Right Circular Blue Border Arrow Buttons -->
      <div
        class="relative"
        @touchstart="onTouchStart"
        @touchend="onTouchEnd"
      >
        <!-- Circular Blue Border Left Arrow Button -->
        <button
          @click="prevProject"
          class="slider-arrow-btn slider-arrow-left"
          aria-label="Projek Sebelumnya"
          title="Projek Sebelumnya (Panah Kiri)"
        >
          <ChevronLeft class="w-6 h-6 transition-transform group-hover:-translate-x-0.5" />
        </button>

        <!-- Circular Blue Border Right Arrow Button -->
        <button
          @click="nextProject"
          class="slider-arrow-btn slider-arrow-right"
          aria-label="Projek Selanjutnya"
          title="Projek Selanjutnya (Panah Kanan)"
        >
          <ChevronRight class="w-6 h-6 transition-transform group-hover:translate-x-0.5" />
        </button>

        <!-- Single Showcase Card with Animated Transition -->
        <div class="project-showcase-wrapper relative">
          <transition name="slide-card" mode="out-in">
            <article
              :key="currentProj.id"
              class="project-card glass-panel rounded-3xl p-6 sm:p-10 border border-white/[0.1] shadow-2xl relative overflow-hidden"
            >
              <!-- Ambient corner glow inside card -->
              <div class="absolute -top-24 -right-24 w-80 h-80 rounded-full bg-sky-500/10 blur-3xl pointer-events-none"></div>

              <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 lg:gap-10 items-center relative z-10">
                
                <!-- Left Info (6 Cols) -->
                <div class="lg:col-span-6 flex flex-col justify-between order-2 lg:order-1">
                  <div>
                    <!-- Badges Row -->
                    <div class="flex flex-wrap items-center gap-2 mb-4">
                      <span class="font-mono text-[11px] font-bold px-3 py-1 rounded-full bg-sky-500/15 border border-sky-500/30 text-sky-300">
                        {{ currentProj.type }}
                      </span>
                      <span class="font-mono text-[11px] px-2.5 py-1 rounded-full bg-white/[0.04] border border-white/[0.08] text-slate-300">
                        {{ currentProj.period }}
                      </span>
                    </div>

                    <!-- Project Title -->
                    <h3 class="font-display font-bold text-2xl sm:text-3xl text-white mb-2 leading-snug">
                      {{ currentProj.title }}
                    </h3>

                    <!-- Institution / Sub-header -->
                    <p class="font-mono text-xs text-sky-400/90 mb-4 flex items-center gap-1.5">
                      <Building2 class="w-3.5 h-3.5" />
                      <span>{{ currentProj.institution }}</span>
                    </p>

                    <!-- Full User Description -->
                    <p class="text-slate-300 text-xs sm:text-sm leading-relaxed mb-6 font-sans">
                      {{ currentProj.description }}
                    </p>

                    <!-- Key Feature Bullets -->
                    <div class="space-y-2 mb-6 p-4 rounded-xl bg-white/[0.02] border border-white/[0.06]">
                      <div class="text-[11px] font-mono font-semibold uppercase tracking-wider text-slate-400 mb-2">
                        Fitur &amp; Kontribusi Utama:
                      </div>
                      <div
                        v-for="(feat, fIdx) in currentProj.keyFeatures"
                        :key="fIdx"
                        class="flex items-start gap-2.5 text-xs text-slate-300"
                      >
                        <span class="w-1.5 h-1.5 rounded-full bg-sky-400 mt-1.5 shrink-0"></span>
                        <span>{{ feat }}</span>
                      </div>
                    </div>

                    <!-- Tags Row -->
                    <div class="flex flex-wrap gap-2 mb-6">
                      <span
                        v-for="(tag, tIdx) in currentProj.tags"
                        :key="tIdx"
                        class="tag-pill"
                      >
                        #{{ tag }}
                      </span>
                    </div>
                  </div>

                  <!-- Action Bar -->
                  <div class="pt-4 border-t border-white/[0.08] flex flex-wrap items-center justify-between gap-4">
                    <button
                      @click="handlePreview(currentProj)"
                      class="btn-secondary text-xs py-2.5 px-4 font-mono flex items-center gap-2 group/btn"
                    >
                      <Maximize2 class="w-3.5 h-3.5 text-sky-400 group-hover/btn:scale-110 transition-transform" />
                      <span>Perbesar Tampilan</span>
                    </button>

                    <div class="text-[11px] font-mono text-slate-400">
                      Role: <span class="text-white">{{ currentProj.role }}</span>
                    </div>
                  </div>

                </div>

                <!-- Right Image Preview (6 Cols) -->
                <div class="lg:col-span-6 order-1 lg:order-2">
                  <div
                    class="relative rounded-2xl overflow-hidden border border-white/[0.12] bg-[#090b10] shadow-2xl cursor-pointer group/img"
                    @click="handlePreview(currentProj)"
                  >
                    <!-- Browser Window Header Mockup -->
                    <div class="flex items-center justify-between px-4 py-2.5 bg-[#12151d] border-b border-white/[0.08]">
                      <div class="flex items-center gap-1.5">
                        <span class="w-2.5 h-2.5 rounded-full bg-red-500/80"></span>
                        <span class="w-2.5 h-2.5 rounded-full bg-yellow-500/80"></span>
                        <span class="w-2.5 h-2.5 rounded-full bg-green-500/80"></span>
                      </div>
                      <span class="font-mono text-[10px] text-slate-400 tracking-wider">
                        {{ currentProj.id }}.system.app
                      </span>
                      <Maximize2 class="w-3 h-3 text-slate-400 group-hover/img:text-sky-400 transition-colors" />
                    </div>

                    <!-- Screenshot Image -->
                    <div class="relative overflow-hidden aspect-video bg-[#07090e] flex items-center justify-center">
                      <img
                        :src="currentProj.image"
                        :alt="currentProj.title"
                        class="w-full h-full object-cover object-top transition-transform duration-500 group-hover/img:scale-105"
                      />
                      <!-- Small magnify hint icon (top-right corner) -->
                      <div class="absolute top-2 right-2 w-6 h-6 rounded-full bg-black/60 backdrop-blur-sm border border-white/20 flex items-center justify-center opacity-0 group-hover/img:opacity-100 transition-opacity duration-300">
                        <Maximize2 class="w-3 h-3 text-white" />
                      </div>
                    </div>

                  </div>
                </div>

              </div>
            </article>
          </transition>
        </div>

        <!-- Bottom High-Visibility Slider Indicator Capsule -->
        <div class="slider-indicators-wrapper flex items-center justify-center">
          <div class="inline-flex flex-wrap items-center justify-center gap-1.5 p-1.5 rounded-2xl bg-[#0e121b] border-2 border-white/[0.12] shadow-2xl backdrop-blur-xl">
            <button
              v-for="(proj, idx) in projects"
              :key="idx"
              @click="selectProject(idx)"
              class="flex items-center gap-2.5 px-3.5 sm:px-4 py-2 rounded-xl text-xs font-mono transition-all duration-300 cursor-pointer border-0"
              :class="currentIndex === idx 
                ? 'bg-sky-500 text-slate-950 font-bold shadow-lg shadow-sky-500/35 scale-[1.02]' 
                : 'bg-white/[0.03] text-slate-400 hover:text-white hover:bg-white/[0.08]'"
              :aria-label="`Pindah ke projek ${proj.tabLabel}`"
            >
              <span
                class="w-2.5 h-2.5 rounded-full shrink-0 transition-all duration-300"
                :class="currentIndex === idx 
                  ? 'bg-slate-950 ring-2 ring-slate-950/30' 
                  : 'bg-sky-500/40 border border-sky-400/60'"
              ></span>
              <span class="tracking-wider">0{{ idx + 1 }} &bull; {{ proj.tabLabel }}</span>
            </button>
          </div>
        </div>

      </div>

    </div>
  </section>
</template>

<style scoped>
/* Circular Blue Border Arrow Buttons positioned directly on Card Borders */
.slider-arrow-btn {
  position: absolute;
  top: 50%;
  z-index: 25;
  width: 44px;
  height: 44px;
  border-radius: 9999px;
  border: 2px solid #38bdf8; /* Blue border */
  background: rgba(9, 11, 16, 0.9);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  color: #38bdf8;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: 0 0 20px rgba(56, 189, 248, 0.3), 0 4px 16px rgba(0, 0, 0, 0.6);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.slider-arrow-btn:hover {
  background: #38bdf8;
  color: #030712;
  box-shadow: 0 0 32px rgba(56, 189, 248, 0.6), 0 6px 20px rgba(0, 0, 0, 0.6);
}

/* Left button centered on card's left border */
.slider-arrow-left {
  left: 0;
  transform: translate(-50%, -50%);
}

.slider-arrow-left:hover {
  transform: translate(-50%, -50%) scale(1.08);
}

.slider-arrow-left:active {
  transform: translate(-50%, -50%) scale(0.95);
}

/* Right button centered on card's right border */
.slider-arrow-right {
  right: 0;
  transform: translate(50%, -50%);
}

.slider-arrow-right:hover {
  transform: translate(50%, -50%) scale(1.08);
}

.slider-arrow-right:active {
  transform: translate(50%, -50%) scale(0.95);
}

@media (min-width: 768px) {
  .slider-arrow-btn {
    width: 52px;
    height: 52px;
  }
}

@media (max-width: 639px) {
  .slider-arrow-btn {
    width: 40px;
    height: 40px;
  }
  .slider-arrow-left {
    left: 4px;
    transform: translateY(-50%);
  }
  .slider-arrow-left:hover {
    transform: translateY(-50%) scale(1.08);
  }
  .slider-arrow-left:active {
    transform: translateY(-50%) scale(0.95);
  }
  .slider-arrow-right {
    right: 4px;
    transform: translateY(-50%);
  }
  .slider-arrow-right:hover {
    transform: translateY(-50%) scale(1.08);
  }
  .slider-arrow-right:active {
    transform: translateY(-50%) scale(0.95);
  }
}

/* Card slide transition */
.slide-card-enter-active,
.slide-card-leave-active {
  transition: all 0.3s ease-out;
}

.slide-card-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

.slide-card-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}

/* Bottom slider indicator capsule balanced spacing */
.slider-indicators-wrapper {
  margin-top: 36px;
}

@media (min-width: 640px) {
  .slider-indicators-wrapper {
    margin-top: 44px;
  }
}
</style>
