<template>
  <div
    class="project p-10 bg-slate-200  m-4 border-[5px] rounded-lg border-l-green-500"
    :class="{ 
        'border-l-green-500': project.complete,  
        'border-l-red-500': !project.complete   }"
  >
    <div class="text-indigo-400" >
      <div class="flex justify-between">
        <div>
          <h3 class="cursor-pointer" @click="showDetail = !showDetail">{{ project.title }}</h3>
        </div>
        <div class="space-x-3">
          <span class="material-symbols-outlined text-green-500 cursor-pointer hover:text-green-700" @click="completeProject(project.id)"> done </span>
          <span class="material-symbols-outlined text-blue-500 cursor-pointer hover:text-blue-700"> edit_square </span>
          <span class="material-symbols-outlined text-red-500 cursor-pointer hover:text-red-700" @click="deleteProject(project.id)"> delete </span>
        </div>
      </div>
    </div>
    <p v-if="showDetail">{{ project.details }}</p>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
      api:'http://localhost:3000/project',
    };
  },
  methods:{
    deleteProject(id){
        fetch(this.api+'/'+id,{
            method: 'Delete',
        }).then(()=>{
            this.$emit('delete',id)
        }).catch((err)=>{
            console.log(err);
        })
    },
    completeProject(id){
        fetch(this.api+'/'+id,{
            method:'PATCH',
            headers: {
                'Content-Type': 'application/json',
            },
            body:JSON.stringify({
                complete:!this.project.complete
            })
        }).then(()=>{
           this.$emit('complete',this.project.id)
        })
    }
  }
};
</script>

<style></style>
