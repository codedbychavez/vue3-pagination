<script>
import users from './data/users'

import Pagination from './components/Pagination.vue'
export default {
  components: {
    Pagination,
  },
  data() {
    return {
      allUsers: users,
      appUsers: [],
      limit: 3,
      activePage: 0,
    }
  },
  methods: {
    fetchUsers(start, end) {
      return this.allUsers.slice(start, end);
    },
  },
  mounted() {
    this.appUsers = this.fetchUsers(this.startIndex, this.endIndex);
  },
  computed: {
    pageCount() {
      return this.allUsers.length / this.limit
    },
    startIndex() {
      return this.activePage * this.limit;
    },
    endIndex() {
      return this.startIndex + this.limit
    },
  },
  watch: {
    activePage() {
        this.appUsers = this.fetchUsers(this.startIndex, this.endIndex);
    }
  }
}
</script>

<template>
  <div class="container m-4">
    <h1 class="text-2xl text-center">Pagination Demo</h1>
    <h4 class="text-xl text-center">App Users</h4>
    <div class="border p-2 mb-4">
      <ul>
        <li v-for="user in appUsers" :key="user.id" class=" text-left">
          {{ user.firstName }}
        </li>
      </ul>
    </div>
    <Pagination 
    :pageCount="pageCount"
    :activePage="activePage"
    @setActivePage="(currentActivePage) => activePage = currentActivePage"
    />
  </div>
</template>