<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import { Menu, X, ArrowUpRight } from 'lucide-vue-next'

const isScrolled = ref(false)
const activeSection = ref('about')
const isMobileMenuOpen = ref(false)
// Flag untuk mencegah IntersectionObserver override saat user klik nav
let isManualScroll = false
let manualScrollTimer: number | null = null

const navItems = [
  { label: 'Tentang', href: '#about', id: 'about' },
  { label: 'Keahlian', href: '#skills', id: 'skills' },
  { label: 'Projek & Pengalaman', href: '#projects', id: 'projects' },
  { label: 'Sertifikat', href: '#certificate', id: 'certificate' },
]


// Scroll handler hanya untuk isScrolled (navbar background)
const handleScroll = () => {
  isScrolled.value = window.scrollY > 40

  // Jika tidak sedang manual scroll, deteksi section aktif via getBoundingClientRect
  if (!isManualScroll) {
    updateActiveSectionByPosition()
  }
}

// Deteksi section aktif berdasarkan posisi scroll dokumen yang stabil
const updateActiveSectionByPosition = () => {
  // Jika sedang klik navigasi manual, jangan ditimpa
  if (isManualScroll) return

  // 1. Cek jika user sudah scroll sampai ke ujung bawah halaman (Contact)
  const isBottom = window.innerHeight + window.scrollY >= document.documentElement.scrollHeight - 70
  if (isBottom) {
    activeSection.value = 'certificate'
    return
  }

  // 2. Garis pandang viewport pengguna
  const scrollRef = window.scrollY + 250

  // 3. Evaluasi section dari bawah ke atas berdasarkan docTop absolut
  const sections = ['certificate', 'projects', 'skills', 'about']
  for (const id of sections) {
    const el = document.getElementById(id)
    if (!el) continue
    const docTop = el.getBoundingClientRect().top + window.scrollY
    if (scrollRef >= docTop) {
      activeSection.value = id
      return
    }
  }

  activeSection.value = 'about'
}

// Klik navbar: langsung set active + smooth scroll presisi
const scrollTo = (href: string) => {
  isMobileMenuOpen.value = false

  const sectionId = href.replace('#', '')
  const el = document.getElementById(sectionId)
  if (!el) return

  // Langsung tetapkan active section pada tombol yang diklik
  if (navItems.some(item => item.id === sectionId)) {
    activeSection.value = sectionId
  }

  // Kunci flag scroll listener selama animasi berjalan
  isManualScroll = true
  if (manualScrollTimer) clearTimeout(manualScrollTimer)
  manualScrollTimer = window.setTimeout(() => {
    isManualScroll = false
  }, 1200)

  // Hitung offset absolut terhadap navbar (75px)
  const navHeight = 75
  const docTop = el.getBoundingClientRect().top + window.scrollY
  const targetY = Math.max(0, docTop - navHeight)

  window.scrollTo({
    top: targetY,
    behavior: 'smooth'
  })
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  if (manualScrollTimer) clearTimeout(manualScrollTimer)
})
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 py-4 px-4 md:px-8 navbar-wrapper"
    :class="isScrolled ? 'navbar-scrolled py-3' : 'py-4'"
  >
    <div class="site-container flex items-center justify-between">
      <!-- Brand Logo -->
      <a
        href="#about"
        class="flex items-center gap-3 text-decoration-none group"
        @click.prevent="scrollTo('#about')"
      >
        <div class="brand-avatar-box">
          <span class="font-brand text-sky-400 font-bold text-sm tracking-wider">RI</span>
        </div>
        <div class="flex flex-col">
          <div class="flex items-center gap-2">
            <span class="font-brand text-white text-sm md:text-base tracking-wide group-hover:text-sky-400 transition-colors">
              REYNALDY IRSYAD
            </span>
            <span class="pulse-dot" title="Available for work"></span>
          </div>
          <span class="text-[10px] text-slate-400 font-mono tracking-wider uppercase hidden sm:block">
            System &amp; Business Analyst
          </span>
        </div>
      </a>

      <!-- Desktop Navigation Menu -->
      <nav class="hidden md:flex items-center gap-1 bg-white/[0.03] border border-white/[0.08] rounded-full p-1.5 backdrop-blur-md">
        <a
          v-for="item in navItems"
          :key="item.id"
          :href="item.href"
          @click.prevent="scrollTo(item.href)"
          class="nav-link px-4 py-2 rounded-full text-xs font-medium tracking-wide transition-all duration-200"
          :class="activeSection === item.id ? 'bg-sky-500/20 text-sky-300 border border-sky-500/40 shadow-sm shadow-sky-500/20' : 'text-slate-300 hover:text-white hover:bg-white/[0.06]'"
        >
          {{ item.label }}
        </a>
      </nav>

      <!-- Right CTAs -->
      <div class="hidden md:flex items-center gap-3">
        <a
          href="#contact"
          @click.prevent="scrollTo('#contact')"
          class="btn-primary text-xs py-2 px-4 shadow-none"
        >
          <span>Kontak</span>
          <ArrowUpRight class="w-3.5 h-3.5" />
        </a>
      </div>

      <!-- Mobile Hamburger Button -->
      <button
        @click="isMobileMenuOpen = !isMobileMenuOpen"
        class="md:hidden p-2 rounded-xl bg-white/[0.05] border border-white/[0.1] text-slate-200 hover:text-white transition-colors"
        aria-label="Toggle menu"
      >
        <Menu v-if="!isMobileMenuOpen" class="w-5 h-5" />
        <X v-else class="w-5 h-5" />
      </button>
    </div>

    <!-- Mobile Dropdown Menu -->
    <transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="transform -translate-y-4 opacity-0"
      enter-to-class="transform translate-y-0 opacity-100"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="transform translate-y-0 opacity-100"
      leave-to-class="transform -translate-y-4 opacity-0"
    >
      <div
        v-if="isMobileMenuOpen"
        class="md:hidden mt-3 mx-2 p-4 rounded-2xl bg-[#0f1219]/95 border border-white/[0.12] backdrop-blur-2xl shadow-2xl flex flex-col gap-2"
      >
        <a
          v-for="item in navItems"
          :key="item.id"
          :href="item.href"
          @click.prevent="scrollTo(item.href)"
          class="px-4 py-3 rounded-xl text-sm font-medium transition-all"
          :class="activeSection === item.id ? 'bg-sky-500/20 text-sky-300 font-semibold border border-sky-500/30' : 'text-slate-300 hover:bg-white/[0.05]'"
        >
          {{ item.label }}
        </a>

        <div class="pt-3 border-t border-white/[0.08] flex flex-col gap-2 mt-2">
          <a
            href="#contact"
            @click.prevent="scrollTo('#contact')"
            class="btn-primary text-center justify-center text-xs py-2.5"
          >
            <span>Hubungi Saya</span>
            <ArrowUpRight class="w-3.5 h-3.5" />
          </a>
        </div>
      </div>
    </transition>
  </header>
</template>

<style scoped>
.brand-avatar-box {
  width: 38px;
  height: 38px;
  border-radius: 10px;
  background: linear-gradient(135deg, rgba(56, 189, 248, 0.15), rgba(129, 140, 248, 0.15));
  border: 1px solid rgba(56, 189, 248, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 15px rgba(56, 189, 248, 0.15);
}

.nav-link {
  text-decoration: none;
}

/* Navbar selalu punya backdrop-blur aktif agar tidak ada flash saat toggle */
.navbar-wrapper {
  /* backdrop-blur selalu ON sejak awal — mencegah white flash saat pertama kali aktif */
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  will-change: background-color, box-shadow;
  /* Background & border transparan dulu, lalu transisi ke gelap saat scrolled */
  background-color: rgba(6, 7, 9, 0);
  border-bottom: 1px solid rgba(255, 255, 255, 0);
  box-shadow: none;
  transition:
    background-color 0.35s ease,
    border-color 0.35s ease,
    box-shadow 0.35s ease,
    padding 0.25s ease;
}

/* State saat sudah scroll: background & border muncul smooth */
.navbar-wrapper.navbar-scrolled {
  background-color: rgba(6, 7, 9, 0.82);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow:
    0 4px 32px rgba(0, 0, 0, 0.5),
    0 1px 0 rgba(255, 255, 255, 0.04);
}
</style>
