<template>
  <div class="home">
    <FilterNav
      @filterValue="currentValue = $event"
      :currentValue="currentValue"
    ></FilterNav>
    <div v-for="project in filterProjects" :key="project.id">
      <SingleProject
        :project="project"
        @delete="removeProject"
        @complete="completeProject"
      ></SingleProject>
    </div>
  </div>
</template>

<script>
import FilterNav from "@/components/FilterNav.vue";
import SingleProject from "@/components/SingleProject.vue";
export default {
  name: "HomeView",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      currentValue: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.projects = data;
      });
  },
  computed: {
    filterProjects() {
      if (this.currentValue === "complete") {
        return this.projects.filter((project) => {
          return project.complete;
        });
      }

      if (this.currentValue === "onGoing") {
        return this.projects.filter((project) => {
          return !project.complete;
        });
      }

      return this.projects;
    },
  },
  methods: {
    removeProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    completeProject(id) {
      let findProject = this.projects.find((project) => project.id == id);
      findProject.complete = !findProject.complete;
    },
  },
};
</script>
