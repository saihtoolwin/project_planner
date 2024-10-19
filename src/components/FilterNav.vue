<template>
  <nav
    class="space-x-4 my-5 flex justify-evenly py-2 text-gray-400 bg-white rounded-md shadow-lg w-full"
  >
    <button :class="{'text-gray-700' : currentValue=== 'all'}" @click="filterBy('all')">All</button
    ><button :class="{'text-gray-700' : currentValue=== 'complete'}" @click="filterBy('complete')">Complete</button
    ><button :class="{'text-gray-700' : currentValue=== 'onGoing'}" @click="filterBy('onGoing')">OnGoing</button>
  </nav>
</template>

<script>
export default {
    props:['currentValue'],
    methods:{
        filterBy(value){
           this.$emit('filterValue',value);
        }
    }
};
</script>

<style lang="scss" scoped></style>
