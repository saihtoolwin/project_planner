<template>
  <div class="w-full max-w-lg mx-auto mt-10">
    <form
      @submit.prevent="updateProject"
      class="bg-white shadow-md rounded-lg px-8 pt-6 pb-8 mb-4"
    >
      <h1 class="text-2xl font-bold text-gray-800 mb-6">
        Edit Project {{ $route.params.id }}
      </h1>
      <div class="mb-6">
        <label
          for="project_title"
          class="block text-gray-700 text-sm font-bold mb-2"
          >Project Title</label
        >
        <input
          type="text"
          v-model="title"
          id="project_title"
          class="shadow appearance-none border rounded w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:ring-2 focus:ring-blue-500"
        />
      </div>
      <div class="mb-6">
        <label
          for="project_details"
          class="block text-gray-700 text-sm font-bold mb-2"
          >Project Details</label
        >
        <textarea
          id="project_details"
          v-model="details"
          class="shadow appearance-none border rounded w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:ring-2 focus:ring-blue-500 h-32"
        ></textarea>
      </div>
      <div class="flex items-center justify-between">
        <button
          type="submit"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        >
          Update
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
    };
  },
  mounted() {
    const projectId = this.$route.params.id;
    fetch(`http://localhost:3000/projects/${projectId}`)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      })
      .catch((error) => {
        console.error("Fetch error:", error);
      });
  },
  methods: {
    updateProject() {
      fetch(`http://localhost:3000/projects/${this.$route.params.id}`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.title,
          details: this.details,
          complete: false,
        }),
      }).then(()=>{
        this.$router.push({name:'home'})
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
