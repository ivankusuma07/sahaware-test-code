<template>
  <div>
    <b-navbar toggleable="lg" type="light" variant="light">
      <b-navbar-brand to="/">NavBar</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item to="/article">Article</b-nav-item>
          <b-nav-item to="/create">Create</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item @click="Login">Login</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      login: '',
    }
  },
  methods: {
    Login() {
      console.log('hehe')
    },
  },
}
</script>
<style>
.bg-light {
  background: #ffffff;
  box-shadow: 0px 1px 1px rgba(0, 0, 0, 0.25);
}
/* .margin {
  margin-right: -30px;
} */
</style>
