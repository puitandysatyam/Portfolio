<script setup>
import { ref, onMounted } from 'vue'
import Card from 'primevue/card';
import ProgressBar from 'primevue/progressbar';

// State for the animation trigger
const isVisible = ref(false)

// Skills data with proficiency
const skills = ref([
  { name: "Spring Boot", proficiency: 45 },
  { name: "MongoDB", proficiency: 70 },
  { name: "Java", proficiency: 70 },
  { name: "Python", proficiency: 75 },
  { name: "JavaScript", proficiency: 30 },
  { name: "Html & Css", proficiency: 50 },
  { name: "Vue", proficiency: 40 },
  { name: "C", proficiency: 60 },
])

// Logic to calculate average XP (Total Proficiency / Count)
const sum = skills.value.reduce((acc, skill) => acc + skill.proficiency, 0)
const avg_xp = Math.round(sum / skills.value.length)

// Trigger the animation on mount
onMounted(() => {
  isVisible.value = true
})
</script>

<template>
  <div class="min-h-screen w-full bg-slate-950 text-slate-100 p-6 flex items-center justify-center font-mono">

    <TransitionGroup
        name="bento"
        tag="div"
        class="grid grid-cols-12 grid-rows-6 gap-4 w-full h-full max-w-7xl max-h-[900px]"
        v-if="isVisible"
    >

      <div key="stats" class="col-span-7 row-span-2 border border-emerald-500/30 bg-emerald-500/5 rounded-2xl p-6 shadow-[0_0_20px_rgba(16,185,129,0.1)]">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-emerald-400 uppercase tracking-widest text-sm font-bold">Player Stats</h2>
          <span class="text-xs text-emerald-500/50 italic">lvl. 20</span>
        </div>
        <div class="space-y-4">
          <h1 class="text-4xl font-black text-white tracking-tight">SATYAM PUITANDY</h1>
          <div class="space-y-2">
            <div class="flex justify-between text-xs uppercase">
              <span>Overall Progress</span>
              <span>{{ avg_xp }}% XP</span>
            </div>
            <ProgressBar :value="avg_xp" :showValue="false" class="h-2 bg-emerald-900/30" />
          </div>
        </div>
      </div>

      <div key="inventory" class="col-span-5 row-span-4 border border-blue-500/30 bg-blue-500/5 rounded-2xl p-6 overflow-hidden">
        <h2 class="text-blue-400 uppercase tracking-widest text-sm font-bold mb-6">Inventory (Skills)</h2>
        <div class="space-y-5 h-full pb-10 custom-scrollbar overflow-y-auto">
          <div v-for="skill in skills" :key="skill.name" class="group">
            <div class="flex justify-between items-center mb-1">
              <span class="text-sm font-medium group-hover:text-blue-300 transition-colors">{{ skill.name }}</span>
              <span class="text-[10px] text-blue-500/60 font-bold">{{ skill.proficiency }}%</span>
            </div>
            <ProgressBar :value="skill.proficiency" :showValue="false" class="h-1 bg-blue-900/30" />
          </div>
        </div>
      </div>

      <div key="quest" class="col-span-4 row-span-2 border border-orange-500/30 bg-orange-500/5 rounded-2xl p-6 flex flex-col justify-between">
        <h2 class="text-orange-400 uppercase tracking-widest text-sm font-bold">Current Quest</h2>
        <div>
          <h3 class="text-2xl font-bold text-white mb-1">Portfolio V1</h3>
          <div class="flex items-center gap-2">
            <span class="w-2 h-2 rounded-full bg-orange-500 animate-pulse"></span>
            <span class="text-xs text-orange-400/80 uppercase">In Progress</span>
          </div>
        </div>
      </div>

      <div key="quote" class="col-span-3 row-span-2 border border-purple-500/30 bg-purple-500/5 rounded-2xl p-6 flex items-center justify-center text-center italic text-purple-200/70">
        <p class="text-sm">"The best way to predict the future is to implement it."</p>
      </div>

      <div key="loot" class="col-span-7 row-span-2 border border-cyan-500/30 bg-cyan-500/5 rounded-2xl p-6 relative overflow-hidden group">
        <div class="absolute -right-4 -bottom-4 opacity-10 group-hover:opacity-20 transition-opacity">
          <i class="pi pi-database text-9xl"></i>
        </div>
        <h2 class="text-cyan-400 uppercase tracking-widest text-sm font-bold mb-4">Epic Loot (Featured Project)</h2>
        <div class="flex items-start gap-4">
          <div class="p-4 bg-cyan-500/10 rounded-xl border border-cyan-500/20">
            <i class="pi pi-server text-3xl text-cyan-400"></i>
          </div>
          <div>
            <h3 class="text-xl font-bold text-white">Spring-Mongo Data Pipeline</h3>
            <p class="text-xs text-cyan-200/50 mt-1 max-w-sm">High-performance aggregation system for large-scale document tracking.</p>
          </div>
        </div>
      </div>

    </TransitionGroup>
  </div>
</template>

<style scoped>
/* 1. The Entrance Animation Logic */
.bento-enter-active {
  transition: all 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.bento-enter-from {
  opacity: 0;
  transform: scale(0.9) translateY(30px);
}

/* Delaying each box slightly to create a staggered effect */
.bento-enter-active:nth-child(1) { transition-delay: 0.1s; }
.bento-enter-active:nth-child(2) { transition-delay: 0.2s; }
.bento-enter-active:nth-child(3) { transition-delay: 0.3s; }
.bento-enter-active:nth-child(4) { transition-delay: 0.4s; }
.bento-enter-active:nth-child(5) { transition-delay: 0.5s; }

/* 2. Custom Scrollbar for the Skills box */
.custom-scrollbar::-webkit-scrollbar {
  width: 4px;
}
.custom-scrollbar::-webkit-scrollbar-track {
  background: transparent;
}
.custom-scrollbar::-webkit-scrollbar-thumb {
  background: rgba(59, 130, 246, 0.2);
  border-radius: 10px;
}

/* 3. PrimeVue Override - Making progress bars match the gamer theme */
:deep(.p-progressbar) {
  border-radius: 99px;
}
:deep(.p-progressbar-value) {
  background: currentColor; /* Inherits text color for each box */
  transition: width 1.5s ease-in-out;
}
</style>