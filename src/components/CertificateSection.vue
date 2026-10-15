<script setup lang="ts">
import {
  ShieldCheck,
  Building,
  Calendar,
  UserCheck,
  Maximize2,
  ExternalLink
} from 'lucide-vue-next'
import certImg from '../assets/sertifikat.png'

const emit = defineEmits<{
  (e: 'open-modal', payload: { title: string; image: string; caption: string }): void
}>()

const openCertModal = () => {
  emit('open-modal', {
    title: 'Sertifikat Selesai Kerja Praktek Telkom University Jakarta',
    image: certImg,
    caption: 'No. 4420/AKD05/RI-S1-SIKJ/2026 • Diberikan kepada Reynaldy Irsyad'
  })
}
</script>

<template>
  <section id="certificate" class="py-24 relative overflow-hidden">
    <!-- Ambient background glow -->
    <div class="absolute right-0 top-1/2 -translate-y-1/2 w-96 h-96 rounded-full bg-sky-500/10 blur-3xl pointer-events-none"></div>

    <div class="site-container relative z-10">
      
      <!-- Section Header -->
      <div class="mb-14">
        <div>
          <div class="flex items-center gap-2 mb-3">
            <span class="w-8 h-[2px] bg-emerald-400"></span>
            <span class="font-mono text-xs uppercase tracking-wider text-emerald-400 font-semibold">
              03 // CREDENTIALS &amp; TRUSTED BY
            </span>
          </div>
          <h2 class="font-display font-black text-3xl sm:text-4xl md:text-5xl text-white uppercase tracking-tight">
            SERTIFIKASI &amp; <span class="text-gradient-emerald">LEGALITAS</span>
          </h2>
        </div>
      </div>

      <!-- Main Certificate Showcase Card -->
      <div class="glass-panel rounded-3xl p-6 sm:p-10 border border-white/[0.12] bg-gradient-to-b from-[#10141e]/90 to-[#090b10]/95 shadow-2xl relative overflow-hidden">
        
        <!-- Top Verified Badge -->
        <div class="flex flex-wrap items-center justify-between gap-4 pb-6 border-b border-white/[0.08] mb-8">
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-xl bg-emerald-500/15 border border-emerald-500/30 flex items-center justify-center text-emerald-400">
              <ShieldCheck class="w-6 h-6" />
            </div>
            <div>
              <div class="flex items-center gap-2">
                <span class="font-display font-bold text-white text-base sm:text-lg">
                  VERIFIED CREDENTIAL
                </span>
                <span class="px-2 py-0.5 rounded-full text-[10px] font-mono font-bold bg-emerald-500/20 text-emerald-300 border border-emerald-500/40">
                  AUTHENTIC
                </span>
              </div>
              <p class="font-mono text-xs text-slate-400">
                Sertifikat Kerja Praktek Internal Telkom University
              </p>
            </div>
          </div>
        </div>

        <!-- Two Column Layout: Image Left, Verification Details Right -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
          
          <!-- Left: Certificate Preview (7 Cols) -->
          <div class="lg:col-span-7">
            <div
              class="relative rounded-2xl overflow-hidden border border-white/[0.15] shadow-2xl bg-slate-900 group cursor-pointer"
              @click="openCertModal"
            >
              <img
                :src="certImg"
                alt="Sertifikat Selesai Kerja Praktek Reynaldy Irsyad Telkom University"
                class="w-full h-auto object-contain transition-transform duration-500 group-hover:scale-[1.02]"
              />

              <!-- Small magnify hint icon (top-right corner) -->
              <div class="absolute top-2.5 right-2.5 w-7 h-7 rounded-full bg-black/60 backdrop-blur-sm border border-white/20 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                <Maximize2 class="w-3.5 h-3.5 text-white" />
              </div>

              <!-- Gold Ribbon Watermark Badge -->
              <div class="absolute bottom-3 right-3 font-mono text-[10px] bg-black/70 backdrop-blur-md px-2.5 py-1 rounded-md text-amber-300 border border-amber-400/30">
                RESMI TELKOM UNIVERSITY
              </div>
            </div>
          </div>

          <!-- Right: Certificate Official Data (5 Cols) -->
          <div class="lg:col-span-5 flex flex-col justify-between space-y-6">
            
            <div class="space-y-4">
              <!-- Recipient & Cert Number Header -->
              <div>
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-sky-500/10 border border-sky-500/25 font-mono text-xs text-sky-300 font-semibold mb-4">
                  <span>No. 4420/AKD05/RI-S1-SIKJ/2026</span>
                </div>
                <h4 class="font-display font-bold text-2xl text-white tracking-tight">
                  REYNALDY IRSYAD
                </h4>
                <p class="font-mono text-xs text-slate-400 mt-1">
                  Mahasiswa S1 Sistem Informasi &bull; Telkom University
                </p>
              </div>

              <!-- Official Certificate Statement Box -->
              <div class="p-4 rounded-xl bg-white/[0.02] border-l-2 border-emerald-400 text-xs text-slate-300 leading-relaxed font-sans">
                &ldquo;Telah melaksanakan Kerja Praktek Internal selama periode 06 Juli 2026 s.d. 07 September 2026 di prodi S1 Sistem Informasi &ndash; Direktorat Kampus Jakarta Universitas Telkom. Dengan ini dinyatakan telah menyelesaikan kerja praktek dengan baik dan menunjukkan sikap profesional serta kemampuan kerja yang baik.&rdquo;
              </div>

              <!-- Structured Specification Cards -->
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5 pt-1">
                <!-- Instansi -->
                <div class="p-3.5 rounded-xl bg-white/[0.025] border border-white/[0.08] flex items-center gap-3">
                  <div class="w-8 h-8 rounded-lg bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-emerald-400 shrink-0">
                    <Building class="w-4 h-4" />
                  </div>
                  <div>
                    <span class="text-[10px] font-mono text-slate-400 uppercase tracking-wider block">Instansi Penerbit</span>
                    <span class="text-xs font-semibold text-white block">Telkom University Jakarta</span>
                  </div>
                </div>

                <!-- Periode -->
                <div class="p-3.5 rounded-xl bg-white/[0.025] border border-white/[0.08] flex items-center gap-3">
                  <div class="w-8 h-8 rounded-lg bg-amber-500/10 border border-amber-500/20 flex items-center justify-center text-amber-400 shrink-0">
                    <Calendar class="w-4 h-4" />
                  </div>
                  <div>
                    <span class="text-[10px] font-mono text-slate-400 uppercase tracking-wider block">Periode Pelaksanaan</span>
                    <span class="text-xs font-semibold text-white block">06 Juli &mdash; 07 September 2026</span>
                  </div>
                </div>

                <!-- Pengesah -->
                <div class="sm:col-span-2 p-3.5 rounded-xl bg-white/[0.025] border border-white/[0.08] flex items-start gap-3">
                  <div class="w-8 h-8 rounded-lg bg-sky-500/10 border border-sky-500/20 flex items-center justify-center text-sky-400 shrink-0 mt-0.5">
                    <UserCheck class="w-4 h-4" />
                  </div>
                  <div class="flex-1 min-w-0">
                    <span class="text-[10px] font-mono text-slate-400 uppercase tracking-wider block">Disahkan Oleh</span>
                    <div class="text-xs font-bold text-white mt-0.5 leading-snug">
                      Qilbaaini Effendi Muftikhali, S.Kom., M.Kom.
                    </div>
                    <div class="text-[11px] font-mono text-slate-400 mt-1 flex flex-wrap items-center gap-x-2 gap-y-0.5">
                      <span>Kaprodi S1 Sistem Informasi</span>
                      <span class="text-slate-600">&bull;</span>
                      <span class="text-sky-400 font-medium">NIP: 25930036</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Action buttons -->
            <div class="pt-4 border-t border-white/[0.08] flex flex-wrap gap-3">
              <button
                @click="openCertModal"
                class="btn-primary text-xs py-2.5 px-4"
              >
                <Maximize2 class="w-3.5 h-3.5" />
                <span>Lihat Sertifikat Resolusi Penuh</span>
              </button>

              <a
                href="/sertifikat-kp.pdf"
                target="_blank"
                class="btn-secondary text-xs py-2.5 px-4"
              >
                <ExternalLink class="w-3.5 h-3.5 text-slate-300" />
                <span>Buka Dokumen PDF</span>
              </a>
            </div>

          </div>

        </div>

      </div>

    </div>
  </section>
</template>
