<script setup lang="ts">
import { ref } from 'vue'
import {
  Mail,
  Phone,
  Instagram,
  Copy,
  Check,
  Send,
  MessageSquare,
  ExternalLink
} from 'lucide-vue-next'

const copiedItem = ref<string | null>(null)

const senderName = ref('')
const selectedTopic = ref('Kolaborasi Projek')
const messageText = ref('')

const copyToClipboard = async (text: string, label: string) => {
  try {
    await navigator.clipboard.writeText(text)
    copiedItem.value = label
    setTimeout(() => {
      copiedItem.value = null
    }, 2200)
  } catch (err) {
    console.error('Failed to copy', err)
  }
}

const sendViaWhatsApp = () => {
  const name = senderName.value.trim() || 'Pengunjung Website'
  const topic = selectedTopic.value
  const msg = messageText.value.trim() || 'Halo Reynaldy, saya tertarik untuk mendiskusikan peluang kerja sama / projek dengan Anda.'

  const formatted = `Halo Reynaldy, saya ${name}.\n\nTopik: ${topic}\nPesan:\n${msg}`
  const url = `https://wa.me/6287789714031?text=${encodeURIComponent(formatted)}`
  window.open(url, '_blank')
}

const sendViaEmail = () => {
  const name = senderName.value.trim() || 'Pengunjung Website'
  const topic = selectedTopic.value
  const msg = messageText.value.trim() || 'Halo Reynaldy, saya tertarik untuk mendiskusikan peluang kerja sama.'

  const subject = `[Portfolio Contact] ${topic} dari ${name}`
  const body = `Halo Reynaldy,\n\nNama: ${name}\nTopik: ${topic}\n\nPesan:\n${msg}\n\nTerima kasih.`
  const url = `mailto:reynalde168@gmail.com?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`
  window.location.href = url
}
</script>

<template>
  <section id="contact" class="py-24 relative overflow-hidden">
    <!-- Ambient Blur Background -->
    <div class="ambient-orb ambient-orb-1" style="opacity: 0.2;"></div>

    <div class="site-container relative z-10">
      
      <!-- Section Header -->
      <div class="mb-14">
        <div>
          <div class="flex items-center gap-2 mb-3">
            <span class="w-8 h-[2px] bg-sky-400"></span>
            <span class="font-mono text-xs uppercase tracking-wider text-sky-400 font-semibold">
              04 // GET IN TOUCH
            </span>
          </div>
          <h2 class="font-display font-black text-3xl sm:text-4xl md:text-5xl text-white uppercase tracking-tight">
            MARI <span class="text-gradient-cyan">BERKOLABORASI</span>
          </h2>
        </div>
      </div>

      <!-- Main Layout: Cards on Left, Interactive WhatsApp Composer on Right -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
        
        <!-- Left: Quick Contact Channel Cards (5 Cols) -->
        <div class="lg:col-span-5 space-y-4">
          
          <!-- WhatsApp / Phone Card -->
          <div class="glass-panel p-6 rounded-2xl border border-white/[0.1] hover:border-emerald-500/40 transition-all duration-300 relative group">
            <div class="flex items-start justify-between">
              <div class="flex items-center gap-3.5">
                <div class="w-12 h-12 rounded-xl bg-emerald-500/15 border border-emerald-500/30 flex items-center justify-center text-emerald-400">
                  <Phone class="w-5 h-5" />
                </div>
                <div>
                  <span class="font-mono text-[11px] text-slate-400 uppercase tracking-wider block">
                    WhatsApp &bull; Phone
                  </span>
                  <a
                    href="https://wa.me/6287789714031"
                    target="_blank"
                    class="font-display font-bold text-white text-base sm:text-lg hover:text-emerald-400 transition-colors"
                  >
                    +62 877-8971-4031
                  </a>
                </div>
              </div>

              <!-- Copy Button -->
              <button
                @click="copyToClipboard('+6287789714031', 'phone')"
                class="p-2.5 rounded-lg bg-white/[0.04] hover:bg-white/[0.1] text-slate-400 hover:text-white transition-all"
                title="Salin Nomor"
              >
                <Check v-if="copiedItem === 'phone'" class="w-4 h-4 text-emerald-400" />
                <Copy v-else class="w-4 h-4" />
              </button>
            </div>

            <div class="mt-4 pt-4 border-t border-white/[0.06] flex items-center justify-between text-xs">
              <span class="text-slate-400 font-mono">Respon Cepat (Aktif)</span>
              <a
                href="https://wa.me/6287789714031"
                target="_blank"
                class="text-emerald-400 hover:underline flex items-center gap-1 font-semibold"
              >
                <span>Buka WhatsApp</span>
                <ExternalLink class="w-3 h-3" />
              </a>
            </div>
          </div>

          <!-- Email Card -->
          <div class="glass-panel p-6 rounded-2xl border border-white/[0.1] hover:border-sky-500/40 transition-all duration-300 relative group">
            <div class="flex items-start justify-between">
              <div class="flex items-center gap-3.5">
                <div class="w-12 h-12 rounded-xl bg-sky-500/15 border border-sky-500/30 flex items-center justify-center text-sky-400">
                  <Mail class="w-5 h-5" />
                </div>
                <div>
                  <span class="font-mono text-[11px] text-slate-400 uppercase tracking-wider block">
                    Email Resmi
                  </span>
                  <a
                    href="mailto:reynalde168@gmail.com"
                    class="font-display font-bold text-white text-base sm:text-lg hover:text-sky-400 transition-colors break-all"
                  >
                    reynalde168@gmail.com
                  </a>
                </div>
              </div>

              <!-- Copy Button -->
              <button
                @click="copyToClipboard('reynalde168@gmail.com', 'email')"
                class="p-2.5 rounded-lg bg-white/[0.04] hover:bg-white/[0.1] text-slate-400 hover:text-white transition-all shrink-0"
                title="Salin Email"
              >
                <Check v-if="copiedItem === 'email'" class="w-4 h-4 text-emerald-400" />
                <Copy v-else class="w-4 h-4" />
              </button>
            </div>

            <div class="mt-4 pt-4 border-t border-white/[0.06] flex items-center justify-between text-xs">
              <span class="text-slate-400 font-mono">Untuk Dokumen &amp; Proposal</span>
              <a
                href="mailto:reynalde168@gmail.com"
                class="text-sky-400 hover:underline flex items-center gap-1 font-semibold"
              >
                <span>Kirim Email Langsung</span>
                <ExternalLink class="w-3 h-3" />
              </a>
            </div>
          </div>

          <!-- Instagram Card -->
          <div class="glass-panel p-6 rounded-2xl border border-white/[0.1] hover:border-pink-500/40 transition-all duration-300 relative group">
            <div class="flex items-start justify-between">
              <div class="flex items-center gap-3.5">
                <div class="w-12 h-12 rounded-xl bg-pink-500/15 border border-pink-500/30 flex items-center justify-center text-pink-400">
                  <Instagram class="w-5 h-5" />
                </div>
                <div>
                  <span class="font-mono text-[11px] text-slate-400 uppercase tracking-wider block">
                    Social Media
                  </span>
                  <a
                    href="https://instagram.com/reynaldy.irsyd"
                    target="_blank"
                    class="font-display font-bold text-white text-base sm:text-lg hover:text-pink-400 transition-colors"
                  >
                    @reynaldy.irsyd
                  </a>
                </div>
              </div>

              <!-- Copy Button -->
              <button
                @click="copyToClipboard('@reynaldy.irsyd', 'instagram')"
                class="p-2.5 rounded-lg bg-white/[0.04] hover:bg-white/[0.1] text-slate-400 hover:text-white transition-all"
                title="Salin Username"
              >
                <Check v-if="copiedItem === 'instagram'" class="w-4 h-4 text-emerald-400" />
                <Copy v-else class="w-4 h-4" />
              </button>
            </div>

            <div class="mt-4 pt-4 border-t border-white/[0.06] flex items-center justify-between text-xs">
              <span class="text-slate-400 font-mono">Koneksi Personal &amp; Aktivitas</span>
              <a
                href="https://instagram.com/reynaldy.irsyd"
                target="_blank"
                class="text-pink-400 hover:underline flex items-center gap-1 font-semibold"
              >
                <span>Follow di Instagram</span>
                <ExternalLink class="w-3 h-3" />
              </a>
            </div>
          </div>

        </div>

        <!-- Right: Interactive Message Composer (7 Cols) -->
        <div class="lg:col-span-7">
          <div class="glass-panel p-6 sm:p-10 rounded-3xl border border-white/[0.12] bg-[#0c0f16]/90 relative">
            
            <div class="flex items-center justify-between mb-6">
              <div class="flex items-center gap-2">
                <MessageSquare class="w-5 h-5 text-sky-400" />
                <h3 class="font-display font-bold text-xl text-white">
                  Kirim Pesan Cepat
                </h3>
              </div>
              <span class="font-mono text-[11px] text-slate-400 bg-white/[0.05] px-2.5 py-1 rounded-full border border-white/[0.08]">
                Instan via WhatsApp / Mail
              </span>
            </div>

            <form @submit.prevent="sendViaWhatsApp" class="space-y-5">
              <!-- Name Input -->
              <div>
                <label class="block font-mono text-xs text-slate-300 uppercase tracking-wider mb-2">
                  Nama Anda / Perusahaan:
                </label>
                <input
                  v-model="senderName"
                  type="text"
                  placeholder="Misal: Budi Santoso (PT Inovasi)"
                  class="w-full px-4 py-3 rounded-xl bg-white/[0.04] border border-white/[0.1] focus:border-sky-400 focus:outline-none focus:ring-1 focus:ring-sky-400 text-white placeholder-slate-500 font-sans text-sm transition-all"
                />
              </div>

              <!-- Topic Selection -->
              <div>
                <label class="block font-mono text-xs text-slate-300 uppercase tracking-wider mb-2">
                  Topik Kebutuhan:
                </label>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                  <button
                    type="button"
                    v-for="topic in ['Kolaborasi Projek', 'Peluang Kerja / Magang', 'Konsultasi Sistem']"
                    :key="topic"
                    @click="selectedTopic = topic"
                    class="py-2.5 px-3 rounded-xl text-xs font-mono transition-all text-center"
                    :class="selectedTopic === topic ? 'bg-sky-500/20 text-sky-300 border border-sky-400/50 font-semibold' : 'bg-white/[0.03] text-slate-400 border border-white/[0.06] hover:bg-white/[0.06]'"
                  >
                    {{ topic }}
                  </button>
                </div>
              </div>

              <!-- Message Input -->
              <div>
                <label class="block font-mono text-xs text-slate-300 uppercase tracking-wider mb-2">
                  Pesan Anda:
                </label>
                <textarea
                  v-model="messageText"
                  rows="4"
                  placeholder="Tuliskan rencana, kebutuhan sistem, atau pertanyaan Anda..."
                  class="w-full px-4 py-3 rounded-xl bg-white/[0.04] border border-white/[0.1] focus:border-sky-400 focus:outline-none focus:ring-1 focus:ring-sky-400 text-white placeholder-slate-500 font-sans text-sm transition-all resize-none"
                ></textarea>
              </div>

              <!-- Action Buttons -->
              <div class="pt-2 flex flex-col sm:flex-row items-center gap-3">
                <button
                  type="submit"
                  class="btn-primary w-full sm:w-auto text-xs py-3 px-6 flex items-center justify-center gap-2"
                >
                  <Send class="w-4 h-4" />
                  <span>Kirim Langsung ke WhatsApp</span>
                </button>

                <button
                  type="button"
                  @click="sendViaEmail"
                  class="btn-secondary w-full sm:w-auto text-xs py-3 px-6 flex items-center justify-center gap-2"
                >
                  <Mail class="w-4 h-4" />
                  <span>Kirim via Email Client</span>
                </button>
              </div>
            </form>

            <!-- Toast alert for copied notification -->
            <transition
              enter-active-class="transition duration-200 ease-out"
              enter-from-class="transform translate-y-2 opacity-0"
              enter-to-class="transform translate-y-0 opacity-100"
              leave-active-class="transition duration-150 ease-in"
              leave-from-class="transform translate-y-0 opacity-100"
              leave-to-class="transform translate-y-2 opacity-0"
            >
              <div
                v-if="copiedItem"
                class="absolute bottom-4 right-4 z-30 px-4 py-2 rounded-xl bg-emerald-500/90 text-slate-950 font-mono text-xs font-bold shadow-2xl flex items-center gap-2"
              >
                <Check class="w-4 h-4" />
                <span>Berhasil disalin ke clipboard!</span>
              </div>
            </transition>

          </div>
        </div>

      </div>

    </div>
  </section>
</template>
