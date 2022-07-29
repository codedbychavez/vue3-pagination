<script>
export default {
  props: {
    activePage: Number,
    pageCount: Number,
  },
  methods: {
    computeActivePage(activePage) {
      console.log(activePage);
      if (activePage < 1) {
        return 0
      }
      if (activePage > this.pageCount - 1) {
        return this.pageCount - 1
      }
      return activePage;
    }
  },
  computed: {
    pageNumbers() {
      return [...Array(this.pageCount).keys()];
    }
  }
}
</script>

<template>
  <div>
    <button class="border rounded-l-xl p-1 hover:bg-gray-100" @click="$emit('setActivePage', computeActivePage(activePage - 1))">Previous</button>
    <ul class="inline-flex">
      <li v-for="pageNumber in pageNumbers" :key="pageNumber" class="border py-1 px-2 hover:bg-gray-100 cursor-pointer" :class="[
        activePage == pageNumber ? 'bg-green-200' : ''
      ]">{{ pageNumber + 1 }}</li>
    </ul>
    <button class="border rounded-r-xl p-1 hover:bg-gray-100" @click="$emit('setActivePage', computeActivePage(activePage + 1))">Next</button>
  </div>
</template>

<style>

</style>