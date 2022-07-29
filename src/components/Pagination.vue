<script>
export default {
  props: {
    activePage: Number,
    pageCount: Number,
  },
  data() {
    return {
      offset: 8,
    };
  },
  methods: {
    computeActivePage(activePage) {
      console.log(activePage);
      if (activePage < 1) {
        return 0;
      }
      if (activePage > this.pageCount - 1) {
        return this.pageCount - 1;
      }
      return activePage;
    },
  },
  computed: {
    pageNumbers() {
      return [...Array(this.pageCount).keys()];
    },
  },
};
</script>

<template>
  <div class="inline-flex">
    <button
      class="rounded-l-xl"
      @click="$emit('setActivePage', computeActivePage(activePage - 1))"
    >
      Previous
    </button>

    <div
      class="flex-wrapper"
      :style="{
        'max-width': (offset - 2) * 100 + 'px',
        'min-width': (offset - 2) * 100 + 'px',
      }"
    >
      <div
        @click="$emit('setActivePage', computeActivePage(0))"
        v-if="activePage >= offset + 1"
        class="page-number"
      >
        1
      </div>

      <div v-if="activePage >= offset + offset - 2">...</div>

      <div v-for="pageNumber in pageNumbers" :key="pageNumber">
        <div
          @click="$emit('setActivePage', computeActivePage(pageNumber))"
          class="page-number"
          :class="[activePage == pageNumber ? 'active' : '']"
          v-if="
            pageNumber >= activePage - offset &&
            pageNumber <= activePage + offset
          "
        >
          {{ pageNumber + 1 }}
        </div>
      </div>
      <div v-if="activePage + offset <= pageCount - offset + 1">...</div>
      <div
        @click="$emit('setActivePage', computeActivePage(pageCount))"
        v-if="activePage + offset <= pageCount - offset + 2"
        class="page-number"
      >
        {{ pageCount }}
      </div>
    </div>
    <button
      class="rounded-r-xl"
      @click="$emit('setActivePage', computeActivePage(activePage + 1))"
    >
      Next
    </button>
  </div>
</template>
