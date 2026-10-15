<script setup lang="ts">
import { ref } from 'vue'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import Marquee from './components/Marquee.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import CertificateSection from './components/CertificateSection.vue'
import ContactSection from './components/ContactSection.vue'
import ImageModal from './components/ImageModal.vue'
import Footer from './components/Footer.vue'

// Modal Lightbox State
const isModalOpen = ref(false)
const modalTitle = ref('')
const modalImage = ref('')
const modalCaption = ref('')

const handleOpenModal = (payload: { title: string; image: string; caption: string }) => {
  modalTitle.value = payload.title
  modalImage.value = payload.image
  modalCaption.value = payload.caption
  isModalOpen.value = true
}

const handleCloseModal = () => {
  isModalOpen.value = false
}
</script>

<template>
  <div class="relative min-h-screen bg-[#060709] text-slate-100 selection:bg-sky-500/30 selection:text-sky-200">
    
    <!-- Background Ambient Atmosphere (Plain dark with soft glowing orbs) -->
    <div class="ambient-orb ambient-orb-1"></div>
    <div class="ambient-orb ambient-orb-2"></div>
    <div class="ambient-orb ambient-orb-3"></div>

    <!-- Main Content Flow -->
    <Navbar />

    <main class="relative z-10">
      <Hero />
      <Marquee />
      <SkillsSection />
      <ProjectsSection @open-modal="handleOpenModal" />
      <CertificateSection @open-modal="handleOpenModal" />
      <ContactSection />
    </main>

    <Footer />

    <!-- Fullscreen Lightbox Modal -->
    <ImageModal
      :is-open="isModalOpen"
      :title="modalTitle"
      :image="modalImage"
      :caption="modalCaption"
      @close="handleCloseModal"
    />

  </div>
</template>

<style scoped>
/* Page layout styles */
</style>
