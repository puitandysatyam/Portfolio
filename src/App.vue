<script setup>
import { ref, onMounted, computed } from 'vue'
import ProgressBar from 'primevue/progressbar';

const isVisible = ref(false)

const skills = ref([
  { name: "Spring Boot", proficiency: 90 },
  { name: "MongoDB", proficiency: 85 },
  { name: "Java", proficiency: 80 },
  { name: "Python", proficiency: 60 },
  { name: "JavaScript", proficiency: 50 },
  { name: "Vue.js", proficiency: 45 },
])

const techStack = ref([
  { name: "Java", icon: "pi pi-server", color: "text-red-400" },
  { name: "Spring", icon: "pi pi-bolt", color: "text-green-400" },
  { name: "Mongo", icon: "pi pi-database", color: "text-emerald-400" },
  { name: "Vue", icon: "pi pi-desktop", color: "text-emerald-300" },
  { name: "JS", icon: "pi pi-code", color: "text-yellow-300" },
  { name: "Git", icon: "pi pi-github", color: "text-white" }
])

const totalXP = computed(() => skills.value.reduce((acc, skill) => acc + skill.proficiency, 0))
const avgXP = computed(() => Math.round(totalXP.value / skills.value.length))

onMounted(() => {
    setTimeout(() => {
    isVisible.value = true
  }, 100)
})
</script>

<template>
  <div class="min-h-screen w-full bg-slate-950 text-slate-100 p-4 lg:p-8 flex items-center justify-center font-mono selection:bg-emerald-500/30">
    
    <TransitionGroup 
      name="bento" 
      tag="div" 
      class="grid grid-cols-1 lg:grid-cols-12 lg:grid-rows-6 gap-6 w-full max-w-[1600px] h-auto lg:h-[85vh]"
      v-if="isVisible"
    >
      
      <div key="stats" class="lg:col-span-7 lg:row-span-2 border-2 border-emerald-500/30 bg-emerald-500/5 rounded-3xl p-6 lg:p-8 flex flex-col justify-between shadow-[0_0_20px_rgba(16,185,129,0.1)]">
        <div>
           <h2 class="text-emerald-400 text-sm font-bold tracking-[0.2em] mb-3 uppercase flex items-center gap-3">
              <i class="pi pi-id-card text-lg"></i> Character Stats
           </h2>
           <h1 class="text-4xl lg:text-7xl font-black tracking-tight text-white mb-2">SATYAM</h1>
           <p class="text-emerald-500/60 text-sm lg:text-lg uppercase italic font-bold">Lvl. 20 Backend Architect</p>
        </div>
        <div class="space-y-3 mt-6 lg:mt-0">
          <div class="flex justify-between text-sm uppercase font-bold text-emerald-200/80">
            <span>XP Progress</span>
            <span>{{ avgXP }}%</span>
          </div>
          <ProgressBar :value="avgXP" :showValue="false" class="h-4 bg-emerald-900/30" />
        </div>
      </div>

      <div key="inventory" class="lg:col-span-5 lg:row-span-4 border-2 border-blue-500/30 bg-blue-500/5 rounded-3xl p-6 lg:p-8 flex flex-col shadow-[0_0_20px_rgba(59,130,246,0.1)] min-h-[400px] lg:min-h-0">
        <h2 class="text-blue-400 text-sm font-bold tracking-[0.2em] mb-6 uppercase flex items-center gap-3">
          <i class="pi pi-box text-lg"></i> Inventory (Skills)
        </h2>
        <div class="space-y-5 overflow-y-auto pr-2 custom-scrollbar flex-1">
          <div v-for="skill in skills" :key="skill.name" class="group">
            <div class="flex justify-between text-sm uppercase mb-1 font-bold tracking-wider">
              <span class="group-hover:text-blue-300 transition-colors text-base">{{ skill.name }}</span>
              <span class="text-blue-500/60">{{ skill.proficiency }}%</span>
            </div>
            <ProgressBar :value="skill.proficiency" :showValue="false" class="h-2.5 bg-blue-900/20" />
          </div>
        </div>
      </div>

      <div key="quest" class="lg:col-span-4 lg:row-span-2 border-2 border-orange-500/30 bg-orange-500/5 rounded-3xl p-6 lg:p-8 flex flex-col justify-between min-h-[220px] lg:min-h-0">
        <h2 class="text-orange-400 text-sm font-bold tracking-[0.2em] uppercase flex items-center gap-3">
          <i class="pi pi-compass text-lg"></i> Current Quest
        </h2>
        <div>
          <h3 class="text-3xl lg:text-4xl font-bold text-white mb-3">Portfolio V1</h3>
          <div class="flex items-center gap-3">
            <span class="relative flex h-3 w-3">
              <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-orange-400 opacity-75"></span>
              <span class="relative inline-flex rounded-full h-3 w-3 bg-orange-500"></span>
            </span>
            <span class="text-sm text-orange-400/80 uppercase font-bold tracking-widest">Active Mission</span>
          </div>
        </div>
      </div>

      <div key="tech" class="lg:col-span-3 lg:row-span-2 border-2 border-pink-500/30 bg-pink-500/5 rounded-3xl p-6 flex flex-col shadow-[0_0_20px_rgba(236,72,153,0.1)]">
        <h2 class="text-pink-400 text-sm font-bold tracking-[0.2em] uppercase mb-4 flex items-center gap-3 shrink-0">
          <i class="pi pi-microchip text-lg"></i> Loadout
        </h2>
        
        <div class="grid grid-cols-3 gap-2 flex-1 place-items-center">
          <div v-for="tech in techStack" :key="tech.name" class="flex flex-col items-center justify-center gap-2 group w-full">
            <i :class="[tech.icon, tech.color, '!text-4xl lg:!text-5xl transition-all duration-300 group-hover:scale-110 group-hover:drop-shadow-[0_0_10px_currentColor]']"></i>
            <span class="text-[10px] font-bold uppercase text-pink-200/50 group-hover:text-pink-200 transition-colors text-center">
              {{ tech.name }}
            </span>
          </div>
        </div>
      </div>

      <div key="quote" class="lg:col-span-5 lg:row-span-2 border-2 border-purple-500/30 bg-purple-500/5 rounded-3xl p-6 lg:p-8 flex flex-col justify-center text-center relative overflow-hidden min-h-[200px] lg:min-h-0">
        <div class="absolute top-4 left-6 text-purple-500/10 text-6xl">
           <i class="pi pi-comments"></i>
        </div>
        <p class="text-purple-200/80 text-lg lg:text-xl italic leading-relaxed z-10 font-medium">
          "Code is like humor. When you have to explain it, it’s bad."
        </p>
      </div>

      <div key="loot" class="lg:col-span-7 lg:row-span-2 border-2 border-cyan-500/30 bg-cyan-500/5 rounded-3xl p-6 lg:p-8 shadow-[0_0_20px_rgba(6,182,212,0.1)] group relative overflow-hidden flex flex-col justify-between min-h-[250px] lg:min-h-0">
        
        <div class="absolute -right-16 -bottom-16 text-cyan-500/5 transition-transform group-hover:rotate-12 duration-700">
           <i class="pi pi-database" style="font-size: 15rem;"></i>
        </div>
        
        <h2 class="text-cyan-400 text-sm font-bold tracking-[0.2em] uppercase mb-4 flex items-center gap-3 z-10">
          <i class="pi pi-trophy text-lg"></i> Epic Loot (Featured)
        </h2>
        
        <div class="flex flex-col lg:flex-row items-start lg:items-center gap-6 z-10">
          <div class="w-16 h-16 lg:w-20 lg:h-20 bg-cyan-400/10 rounded-2xl flex items-center justify-center border border-cyan-400/20 shrink-0">
            <i class="pi pi-server text-3xl lg:text-4xl text-cyan-400"></i>
          </div>
          <div>
            <h3 class="text-2xl lg:text-3xl font-bold text-white mb-2">Spring-Mongo API</h3>
            <p class="text-xs lg:text-sm text-cyan-400/60 tracking-widest uppercase font-bold">High Performance Data Aggregator</p>
          </div>
        </div>
      </div>

    </TransitionGroup>
  </div>
</template>

<style scoped>
/* 1. The Animation Name 'bento' MUST match <TransitionGroup name="bento"> */
.bento-enter-active {
  transition: all 0.8s cubic-bezier(0.25, 1, 0.5, 1);
}

.bento-enter-from {
  opacity: 0;
  transform: translateY(30px) scale(0.95); /* Starts slightly down and small */
  filter: blur(10px); /* Starts blurry */
}

/* 2. Staggered Delays (This makes them pop in one by one) */
.bento-enter-active:nth-child(1) { transition-delay: 0.1s; } /* Stats */
.bento-enter-active:nth-child(2) { transition-delay: 0.2s; } /* Inventory */
.bento-enter-active:nth-child(3) { transition-delay: 0.3s; } /* Quest */
.bento-enter-active:nth-child(4) { transition-delay: 0.4s; } /* Loadout */
.bento-enter-active:nth-child(5) { transition-delay: 0.5s; } /* Quote */
.bento-enter-active:nth-child(6) { transition-delay: 0.6s; } /* Loot */

/* 3. Scrollbar & Progress Bar Styles */
.custom-scrollbar::-webkit-scrollbar { width: 4px; }
.custom-scrollbar::-webkit-scrollbar-track { background: transparent; }
.custom-scrollbar::-webkit-scrollbar-thumb { background: rgba(59, 130, 246, 0.2); border-radius: 10px; }

:deep(.p-progressbar) { border-radius: 4px; background: rgba(255,255,255,0.05); }
:deep(.p-progressbar-value) { background: currentColor; transition: width 1s ease-out; }
</style>