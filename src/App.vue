<script setup>
  import { ref } from 'vue'
  import Card from 'primevue/card';
  import ProgressBar from 'primevue/progressbar';

  const skills = ref(["Spring Boot", "MongoDB", "Java"])
</script>

<template>
  <section class="p-8"> <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <Card v-for="skill in skills" :key="skill">
        <template #title>{{ skill }}</template>
        <template #content>
          <div class="mt-2">
            <h5 class="text-sm mb-2 text-gray-600">Proficiency</h5>
            <ProgressBar :value="70" :show-value="false" style="height: 6px;"/>
          </div>
        </template>
      </Card>
    </div>
  </section>
</template>