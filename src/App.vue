<script setup>
  import { ref } from 'vue'
  import Card from 'primevue/card';
  import ProgressBar from 'primevue/progressbar';

  const skills = ref([
    {name : "Spring Boot", proficiency : 45, row : "row-span-6", col : "col-span-6"},
    {name : "MongoDB", proficiency : 70, row : "row-span-1", col : "col-span-6"},
    {name : "Java", proficiency : 70, row : "row-span-1", col : "col-span-6"},
    {name : "Python", proficiency : 75, row : "row-span-1", col : "col-span-6"},
    {name : "JavaScript", proficiency : 30, row : "row-span-1", col : "col-span-6"},
    {name : "Html & Css", proficiency : 50, row : "row-span-1", col : "col-span-6"},
    {name : "Vue", proficiency : 40, row : "row-span-1", col : "col-span-6"},
    {name : "C", proficiency : 60, row : "row-span-1", col : "col-span-6"},
  ])
  let sum =0
  const avg_xp = ref(0)
  for (let i =0; i < skills.value.length; i++){
    
    sum = skills.value[i].proficiency + sum
  }
  avg_xp.value = Math.round(sum/skills.value.length)
</script>

<template>
  <div class="grid grid-cols-12 grid-rows-6 gap-4 w-auto h-fill">
    <div class="justify-center items-center col-span-7 row-span-2 border-2 border-green-400 rounded-2xl p-4">
      <p>This is Satyam</p>
      <div class="flex-1 p-4">
        <p>Progress : </p>
        <ProgressBar :value="avg_xp" />
      </div>
    </div> 
    <div class="justify-center items-center col-span-5 row-span-4 border-2 border-green-400 rounded-2xl p-4">
      <template v-for="skill in skills" :key="skill">
        <Card>
          <template #title>{{ skill.name }}</template>
          <template #content>
            <ProgressBar :value="skill.proficiency" />
          </template>
        </Card>
      </template>

    </div>
    <div>

    </div>
    <div>
      
    </div>
    <div>
      
    </div>
  </div>
</template>