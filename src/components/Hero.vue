<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import { ArrowDown, ShieldCheck } from 'lucide-vue-next'
import profileCutout from '../assets/profile-cutout.png'
import telkomLogo from '../assets/telkom-logo.png'

// Dynamic Typing Effect
const roles = [
  'System Analyst',
  'Business Analyst',
  'Web Developer',
  'Business Process Modeler (BPMN)',
  'Data & BI Specialist',
  'Agile Scrum Practitioner'
]

const currentText = ref('')
const currentRoleIndex = ref(0)
const isDeleting = ref(false)
const typingSpeed = ref(80)

let timer: number | null = null

const tick = () => {
  const fullText = roles[currentRoleIndex.value]

  if (isDeleting.value) {
    currentText.value = fullText.substring(0, currentText.value.length - 1)
    typingSpeed.value = 40
  } else {
    currentText.value = fullText.substring(0, currentText.value.length + 1)
    typingSpeed.value = 85
  }

  if (!isDeleting.value && currentText.value === fullText) {
    typingSpeed.value = 1800
    isDeleting.value = true
  } else if (isDeleting.value && currentText.value === '') {
    isDeleting.value = false
    currentRoleIndex.value = (currentRoleIndex.value + 1) % roles.length
    typingSpeed.value = 400
  }

  timer = window.setTimeout(tick, typingSpeed.value)
}

const scrollTo = (targetId: string) => {
  const el = document.getElementById(targetId)
  if (el) {
    const navHeight = 75
    const docTop = el.getBoundingClientRect().top + window.scrollY
    window.scrollTo({
      top: Math.max(0, docTop - navHeight),
      behavior: 'smooth'
    })
  }
}

onMounted(() => {
  timer = window.setTimeout(tick, 500)
})

onUnmounted(() => {
  if (timer) clearTimeout(timer)
})
</script>

<template>
  <section id="about" class="relative pt-32 pb-20 md:pt-40 md:pb-28 overflow-hidden">
    <div class="site-container relative z-10">
      
      <!-- Top Status Pill -->
      <div class="flex items-center gap-3 mb-8">
        <div class="inline-flex items-center gap-2.5 px-3.5 py-1.5 rounded-full bg-white/[0.04] border border-white/[0.08] backdrop-blur-md">
          <span class="pulse-dot"></span>
          <span class="font-mono text-xs uppercase tracking-wider text-slate-300">
            TERBUKA UNTUK KERJA PRAKTIK, PROJEK &amp; KARIR
          </span>
        </div>
      </div>

      <!-- Main Grid Hero: Left Info, Right Portrait -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-8 items-center">
        
        <!-- Left Content (7 Cols on desktop) -->
        <div class="lg:col-span-7 flex flex-col">
          
          <!-- Large Futuristic Name -->
          <div class="mb-4">
            <h1 class="font-display font-black tracking-tight text-white uppercase text-4xl sm:text-6xl md:text-7xl lg:text-7xl leading-[1.05]">
              REYNALDY <br />
              <span class="text-gradient-cyan">IRSYAD</span>
            </h1>
            <div class="mt-3">
              <p class="font-mono text-xs sm:text-sm tracking-wider uppercase text-slate-400">
                S1 Sistem Informasi &bull; Telkom University Kampus Jakarta
              </p>
            </div>
          </div>

          <!-- Dynamic Typing Effect Headline -->
          <div class="my-5 p-3.5 sm:p-4 rounded-xl bg-white/[0.03] border border-white/[0.08] backdrop-blur-md">
            <div class="flex items-center gap-2 text-xs font-mono text-slate-400 mb-1">
              <span class="text-sky-400 font-bold">&gt;_</span>
              <span>ROLE &amp; FOCUS AREA</span>
            </div>
            <div class="font-mono text-lg sm:text-2xl font-bold text-sky-300 min-h-[36px] flex items-center">
              <span>{{ currentText }}</span>
              <span class="typing-cursor"></span>
            </div>
          </div>

          <!-- About Me Description (Exact text from user) -->
          <div class="text-slate-300 text-sm sm:text-base leading-relaxed space-y-4 max-w-2xl">
            <p>
              <strong class="text-white font-semibold">Mahasiswa Sistem Informasi Telkom University</strong> yang berfokus pada 
              <span class="text-sky-300 underline decoration-sky-500/40 decoration-2 underline-offset-4 font-medium">System Analysis</span>, 
              <span class="text-indigo-300 underline decoration-indigo-500/40 decoration-2 underline-offset-4 font-medium">Business Analysis</span>, dan 
              <span class="text-emerald-300 underline decoration-emerald-500/40 decoration-2 underline-offset-4 font-medium">Web Development</span>. 
              Memiliki kemampuan dalam menganalisis kebutuhan bisnis, memetakan proses bisnis, serta merancang dan mengembangkan solusi sistem berbasis website yang sesuai dengan kebutuhan pengguna.
            </p>
            <p class="text-slate-400 text-xs sm:text-sm">
              Mampu menjembatani kebutuhan bisnis dengan solusi teknis melalui pendekatan yang analitis, kolaboratif, dan berorientasi pada pemecahan masalah. Berkomitmen untuk mengembangkan solusi teknologi yang efektif dan tepat guna guna meningkatkan efisiensi proses bisnis, mendukung pengambilan keputusan, serta memberikan dampak positif bagi operasional dan pertumbuhan organisasi.
            </p>
          </div>

          <!-- Quick Action Buttons -->
          <div class="flex flex-wrap items-center gap-4 mt-8">
            <button
              @click="scrollTo('projects')"
              class="btn-primary"
            >
              <span>Eksplorasi Projek</span>
              <ArrowDown class="w-4 h-4" />
            </button>

            <button
              @click="scrollTo('certificate')"
              class="btn-secondary"
            >
              <ShieldCheck class="w-4 h-4 text-sky-400" />
              <span>Verifikasi Sertifikat</span>
            </button>

          </div>

          <!-- Bottom Highlight Stats -->
          <div class="grid grid-cols-3 gap-4 sm:gap-6 pt-8 mt-8 border-t border-white/[0.08] max-w-lg">
            <div>
              <div class="font-display font-bold text-2xl sm:text-3xl text-white">3+</div>
              <div class="text-[11px] sm:text-xs text-slate-400 font-mono mt-0.5">Projek Selesai</div>
            </div>
            <div>
              <div class="font-display font-bold text-2xl sm:text-3xl text-emerald-400">3.84</div>
              <div class="text-[11px] sm:text-xs text-slate-400 font-mono mt-0.5">GPA / IPK</div>
            </div>
            <div>
              <div class="font-display font-bold text-2xl sm:text-3xl text-indigo-400">Sem. 7</div>
              <div class="text-[11px] sm:text-xs text-slate-400 font-mono mt-0.5">Semester Aktif</div>
            </div>
          </div>

        </div>

        <!-- Right Content: Profile Portrait Showcase (5 Cols on desktop) -->
        <div class="lg:col-span-5 relative flex justify-center items-center">
          
          <!-- Ambient Halo Aura Glow behind portrait -->
          <div class="absolute w-72 h-72 sm:w-96 sm:h-96 rounded-full bg-gradient-to-tr from-sky-500/25 via-indigo-500/20 to-purple-500/20 blur-3xl pointer-events-none -z-10"></div>
          
          <!-- Futuristic Framing Elements -->
          <div class="relative w-full max-w-sm sm:max-w-md flex flex-col items-center">
            
            <!-- Corner Reticle Accents -->
            <div class="absolute -top-3 -left-3 w-8 h-8 border-t-2 border-l-2 border-sky-400/60 pointer-events-none z-20"></div>
            <div class="absolute -top-3 -right-3 w-8 h-8 border-t-2 border-r-2 border-sky-400/60 pointer-events-none z-20"></div>
            <div class="absolute -bottom-3 -left-3 w-8 h-8 border-b-2 border-l-2 border-sky-400/60 pointer-events-none z-20"></div>
            <div class="absolute -bottom-3 -right-3 w-8 h-8 border-b-2 border-r-2 border-sky-400/60 pointer-events-none z-20"></div>

            <!-- Profile Image Container with soft gradient fade mask at bottom -->
            <div class="relative overflow-hidden w-full rounded-2xl bg-gradient-to-b from-white/[0.06] via-[#0e131d]/80 to-[#07090e] p-3 sm:p-4 border border-white/[0.12] shadow-2xl">
              
              <!-- Spotlight background -->
              <div class="absolute inset-0 bg-[radial-gradient(circle_at_50%_35%,rgba(56,189,248,0.18)_0%,transparent_70%)] pointer-events-none"></div>

              <div class="relative flex justify-center items-end pt-4">
                <img
                  :src="profileCutout"
                  alt="Reynaldy Irsyad - System Analyst & Web Developer"
                  class="w-full h-auto max-h-[460px] sm:max-h-[500px] object-contain object-bottom profile-fade-bottom transition-transform duration-700 hover:scale-[1.03]"
                  loading="eager"
                />
              </div>


              <!-- Floating Chip: Telkom University -->
              <div class="absolute bottom-6 left-4 z-20 glass-panel px-3.5 py-2 rounded-xl flex items-center gap-2.5 border border-white/[0.12] shadow-xl">
                <img
                  :src="telkomLogo"
                  alt="Logo Telkom University"
                  class="w-6 h-6 object-contain shrink-0"
                />
                <div class="flex flex-col text-left">
                  <span class="text-xs font-semibold text-white">Telkom University</span>
                  <span class="text-[10px] text-slate-400 font-mono">Kampus Jakarta</span>
                </div>
              </div>

            </div>

          </div>

        </div>

      </div>

    </div>
  </section>
</template>

<style scoped>
/* Responsive layout tweaks */
</style>
