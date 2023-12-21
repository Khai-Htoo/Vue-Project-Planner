<template>
  <div class="home">

  <h1 class="text-2xl font-bold mt-12 text-slate-400 mb-4">Today Tasks</h1>
  <NavFilter class="mb-4" @filterValue="current=$event" :current="current"></NavFilter>
      <hr>
<div v-for="project in filtered" :key="project.id">
    <SingleProject :project="project" @delete="deleteProject" @complete="completeProject" ></SingleProject>
</div>
  </div>
</template>

<script>

import NavFilter from '../components/NavFilter'
import SingleProject from './SingleProject'
export default {
  components: {
    NavFilter, SingleProject },
  name: 'HomeView',
  data() {
    return {
      projects: [],
      current:"all"
    }
  },
  methods: {
    deleteProject(id) {
     this.projects = this.projects.filter(project=>{
      return project.id != id
     })
    },
   completeProject(id){
    let findProject = this.projects.find(project=>{
      return project.id === id
    })
    findProject.complete = !findProject.complete
   }

  },
  mounted () {
    fetch('http://localhost:3000/projects').then(((response)=>{
      return response.json()
    })).then((data)=>{
      this.projects = data
    }).catch((err)=>{
      console.log(err);
    })
  },
  computed: {
    filtered() {
      if(this.current === 'Complete'){
          return this.projects.filter((p)=>{
            return p.complete
          })
      }
      if(this.current === 'Ongoing'){
        return this.projects.filter((p)=>{
          return !p.complete
        })
      }
      return this.projects
    }
  },
  
}
</script>
