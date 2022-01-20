<template>
  <div class="wrapper">
    <b-navbar toggleable="md" type="light" variant="light" fixed="top">
      <b-navbar-brand to="/" class="mx-3">
        <div class="d-none d-sm-block">
          <b-img src="/sahaware.png" alt="Left image" fluid></b-img>
        </div>
        <div class="d-xl-none d-md-none d-sm-none">
          <b-row>
            <b-col cols="10">
              <b-img src="/sahaware.png" alt="Left image" fluid></b-img>
            </b-col>
          </b-row>
        </div>
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="text-center">
          <b-nav-item to="/">Home</b-nav-item>
          <b-nav-item to="/article">Article</b-nav-item>
          <b-nav-item to="/create">Create</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto text-center">
          <b-nav-item id="btnLogin" @click="Login">Login</b-nav-item>
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
<style scoped>
.bg-light {
  background: #ffffff;
  box-shadow: 0px 1px 1px rgba(0, 0, 0, 0.25);
}
/* .margin {
  margin-right: -30px;
} */
.nav-item.nav-item.nav-item a {
  color: black;
}
.nav-item.nav-item.nav-item a.nuxt-link-exact-active.nuxt-link-active {
  color: #ed3237;
}
#btnLogin > .nav-link {
  color: #2d9cdb;
}

.navbar-light .navbar-toggler {
  border-color: rgba(0, 0, 0, 0);
}
</style>
