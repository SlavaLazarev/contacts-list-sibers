<template >
  <div>
    <div class="input-group flex-nowrap">
      <span class="input-group-text" id="addon-wrapping">Search</span>
      <input
          v-model="searchQuery"
          type="text"
          class="form-control"
          placeholder="Username"
          aria-label="Username"
          aria-describedby="addon-wrapping">
    </div>
    <br>
    <select v-model="sortingType" class="form-select" aria-label="Default select example">
      <option value="A-Z">Sort A-Z</option>
      <option value="Z-A">Sort Z-A</option>
    </select>
    <br>
    <User
        v-for="user in sortedUsers"
        :key="user.id"
        :user="user"
        :users="users"
    />
  </div>
</template>


<script>
import User from "@/components/User";
export default {
  data() {
    return {
      searchQuery: "",
      sortingType: "A-Z"
    };
  },
  props: ["users"],
  components: {
    User
  },
  computed: {
    filteredUsers() {
      return this.users.filter(
          item => item.name.indexOf(this.searchQuery.trim()) !== -1
      );
    },
    sortedUsers() {
      let filtered = this.filteredUsers.slice();
      if (this.sortingType === "A-Z") {
        return filtered.sort((a, b) => (a.name > b.name ? 1 : -1));
      } else if (this.sortingType === "Z-A") {
        return filtered.sort((a, b) => (a.name > b.name ? -1 : 1));
      } else {
        return filtered.sort((a, b) => (a.id > b.id ? 1 : -1));
      }
    },
  }
};
</script>

