<template>
  <div id="app">
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Contacts</a>
      </div>
    </nav>
    <Users :users="users" />
  </div>
</template>

<script>
import Users from "@/components/Users";
export default {
  name: 'App',
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    if (localStorage.getItem("users")) {
      this.users = JSON.parse(localStorage.getItem("users"));
    } else {
      fetch("http://demo.sibers.com/users")
          .then(response => {
            if (response.ok) {
              return response.json();
            } else {
              response.json().then(err => {
                const error = new Error(
                    "Sorry, something went wrong."
                );
                error.data = err;
                throw error;
              });
            }
          })
          .then(data => {
            this.users = data;
            const parsed = JSON.stringify(this.users);
            localStorage.setItem("users", parsed);
          });
    }
  },
  components: {Users}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}
</style>