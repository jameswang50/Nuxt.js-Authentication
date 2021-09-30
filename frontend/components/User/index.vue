<template>
  <div>
    Hello dear <b style="color:red">{{ getUserInfo.fullname }}</b> you're in
    Users page
    <hr />
    This is all users information:
    <br /><br />
    <table class="table">
      <thead>
        <tr>
          <th scope="col">ID</th>
          <th scope="col">FullName</th>
          <th scope="col">Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user._id">
          <td>{{ user._id }}</td>
          <td>{{ user.fullname }}</td>
          <td>{{ user.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
    }
  },
  computed: {
    getUserInfo() {
      return this.$store.getters.getUserInfo;
    }
  },
  mounted() {
    this.getAllUsers();
  },
  methods: {
    async getAllUsers() {
      try {
        this.users = await this.$axios.$get("/api/auth/users");
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>
