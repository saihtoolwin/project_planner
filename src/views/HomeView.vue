<template>
  <div class="home">
    <div v-for="project in projects" :key="project.id">
     <SingleProject :project="project" @delete="removeProject" @complete="completeProject"></SingleProject>
    </div>
  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue';
export default {
  name: 'HomeView',
  components: {
    SingleProject
  },
  data(){
    return {
      projects:[],
    }
  },
  mounted() {
     fetch('http://localhost:3000/projects').then((response)=>{
      // console.log(response.json());
      return response.json();
    }).then((data)=>{
      this.projects=data;
    })
  },
  methods:{
    removeProject(id){
      this.projects = this.projects.filter(project => project.id !== id);
    },
    completeProject(id){
      let findProject = this.projects.find(project => project.id == id);
      findProject.complete =! findProject.complete;
    }
  }
}
</script>
