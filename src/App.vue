<script setup>
  import { ref } from 'vue'
  import Card from 'primevue/card';
  import ProgressBar from 'primevue/progressbar';

  const skills = ref([
    {name : "Spring Boot", proficiency : "45", },
    {name : "MongoDB", proficiency : "70"},
    {name : "Java", proficiency : "70"},
    {name : "Python", proficiency : "75"},
    {name : "JavaScript", proficiency : "30"},
    {name : "Html & Css", proficiency : "50"},
    {name : "Vue", proficiency : "40"},
    {name : "C", proficiency : "60"},
  ])
</script>

<template>
  <section class="p-8"> 
    <div class="grid grid-cols-16 grid-rows-9 gap-4">
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