<template>
  <nav class="mt-10 p-4 shadow-md text-center">
    <div class="max-w-7xl mx-auto flex justify-center items-center">
      <div class="font-bold text-lg space-x-5 text-center items-center">
        <router-link
          to="/"
          activeClass="text-indigo-500"
          >Projects</router-link
        >
        <router-link
          :to="{ name: 'AddProject' }"
          activeClass="text-indigo-500"
          >Add Project</router-link
        >
      </div>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style scoped></style>
