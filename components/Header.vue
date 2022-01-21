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

        <b-navbar-nav v-if="cookiez != null" class="ml-auto text-center">
          <span class="mt-2 mr-2"> Hi, {{ username }} </span>
          <b-nav-item id="btnLogin" @click="logout">Logout</b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav v-else class="ml-auto text-center">
          <b-nav-item id="btnLogin" @click="loginModal">Login</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <!-- MODAL START-->
    <b-modal
      v-model="modalLogin"
      centered
      title="Login"
      hide-footer
      hide-header
      no-stacking
    >
      <div class="container">
        <div class="modalTitle modalTitles top-left">Login</div>
        <b-button
          variant="link"
          class="closeBtn top-right"
          @click="modalLogin = false"
        >
          &times;
        </b-button>
        <div class="mb-2">
          Don’t have an account?
          <b-link id="link" @click="registerModal">Create account</b-link>
        </div>

        <!-- <b-form @submit="loginSubmit"> -->
        <b-form-group id="input-group-1" label="Email" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="loginForm.email"
            type="email"
            placeholder="Enter your email"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Password" label-for="input-2">
          <b-input-group class="mb-2">
            <b-form-input
              id="input-2"
              :type="passwordField"
              v-model="loginForm.password"
              placeholder="Enter your password"
              v-on:keyup.enter="loginSubmit"
            ></b-form-input>
            <b-input-group-append>
              <b-button
                @click="hideAndShowPass"
                variant="outline-dark"
                size="sm"
              >
                <b-icon :icon="icons"></b-icon>
              </b-button>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>

        <b-button type="button" variant="danger" @click="loginSubmit"
          ><b-spinner v-show="showSpinner" class="mr-2" small></b-spinner>Log
          in</b-button
        >
        <!-- </b-form> -->
      </div>
    </b-modal>

    <b-modal
      v-model="modalRegister"
      centered
      title="Login"
      hide-footer
      hide-header
      no-stacking
    >
      <div class="container">
        <div class="modalTitle modalTitles top-left">Create Account</div>
        <b-button
          variant="link"
          class="closeBtn top-right"
          @click="modalRegister = false"
        >
          &times;
        </b-button>
        <div class="mb-2">
          Have an account?
          <b-link id="link" @click="loginModal">Login</b-link>
        </div>

        <!-- <b-form @submit="loginSubmit"> -->
        <b-form-group id="input-group-1" label="Fullname" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="registerForm.name"
            type="text"
            placeholder="Enter your fullname"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Email" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="registerForm.email"
            type="email"
            placeholder="Enter your email"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Password" label-for="input-3">
          <b-input-group class="mb-2">
            <b-form-input
              id="input-3"
              :type="passwordField"
              v-model="registerForm.password"
              placeholder="Enter your password"
              v-on:keyup.enter="loginSubmit"
            ></b-form-input>
            <b-input-group-append>
              <b-button
                @click="hideAndShowPass"
                variant="outline-dark"
                size="sm"
              >
                <b-icon :icon="icons"></b-icon>
              </b-button>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>

        <b-form-group
          id="input-group-4"
          label="Phone Number"
          label-for="input-4"
        >
          <b-form-input
            id="input-4"
            v-model="registerForm.phone"
            type="number"
            placeholder="Enter your phone number"
            required
          ></b-form-input>
        </b-form-group>

        <b-button type="button" variant="danger" @click="registerSubmit"
          ><b-spinner v-show="showSpinner" class="mr-2" small></b-spinner>Create
          Account</b-button
        >
        <!-- </b-form> -->
      </div>
    </b-modal>
    <!-- MODAL END -->
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      login: '',
      modalLogin: false,
      modalRegister: false,
      show: true,
      loginForm: {
        email: '',
        password: '',
      },
      registerForm: {
        name: '',
        email: '',
        password: '',
        phone: '',
      },
      passwordField: 'password',
      icons: 'eye',
      showSpinner: false,
      username: '',
      cookiez: null,
    }
  },
  watch: {
    cookiez() {
      console.log('cookiez', this.cookiez)
    },
  },
  mounted() {
    // setInterval(() => {
    //   this.cookiez = this.$cookies.get('token')
    //   console.log(this.cookiez)
    // }, 1000)
    // this.cookiez = this.$cookies.get('token')
  },
  methods: {
    loginModal() {
      this.modalLogin = true
      this.resetRegisterForm()
      // this.$toast.success('Success toast')
    },
    registerModal() {
      this.modalRegister = true
      this.resetLoginForm()
    },
    async loginSubmit() {
      this.showSpinner = true
      console.log('login form', this.loginForm)
      await this.$axios
        .post('/api/auth/login', this.loginForm)
        .then((response) => {
          console.log(response.data.content[0])
          // this.username = response.data.content[0].name

          //SET COOKIES
          this.$cookies.set('token', response.data.content[0].token, {
            path: '/',
            maxAge: 60 * 60 * 24,
          })
          this.$cookies.set('username', response.data.content[0].name, {
            path: '/',
            maxAge: 60 * 60 * 24,
          })
          this.$toast.success('Login Success')
          this.cookiez = this.$cookies.get('token')
          this.username = this.$cookies.get('username')
          this.resetLoginForm()
        })
        .catch((err) => {
          if (!err) {
          } else {
            console.log(err.response.data)
            console.log(err.response.status)
            console.log(err.response.headers)
            // this.resetLoginForm()
            this.showSpinner = false
            if (err.response.status === 409) {
              this.$toast.error(err.response.data.message.details[0].message)
            } else {
              this.$toast.error(err.response.data.message)
            }
          }
        })
    },
    async registerSubmit() {
      this.showSpinner = true
      console.log('register form', this.registerForm)
      await this.$axios
        .post('/api/auth/register', this.registerForm)
        .then((response) => {
          console.log(response.data.content[0])
          this.$toast.success('Account has been created')
          this.resetRegisterForm()
        })
        .catch((err) => {
          if (!err) {
          } else {
            console.log(err.response.data)
            console.log(err.response.status)
            console.log(err.response.headers)
            // this.resetRegisterForm()
            this.showSpinner = false
            if (err.response.status === 409) {
              if (
                err.response.data.message ===
                'Data With the same email already exist'
              ) {
                this.$toast.error(err.response.data.message)
              } else {
                this.$toast.error(err.response.data.message.details[0].message)
              }
            } else {
              this.$toast.error(err.response.data.message)
            }
          }
        })
    },
    logout() {
      this.$cookies.remove('token')
      this.$cookies.remove('username')
      this.cookiez = null
      this.$toast.success('Logout Success')
    },
    hideAndShowPass() {
      console.log('masuk')
      this.passwordField == 'password'
        ? (this.passwordField = 'text')
        : (this.passwordField = 'password')
      this.icons == 'eye' ? (this.icons = 'eye-slash') : (this.icons = 'eye')
    },
    resetLoginForm() {
      this.showSpinner = false
      this.modalLogin = false
      this.loginForm.email = ''
      this.loginForm.password = ''
    },
    resetRegisterForm() {
      this.showSpinner = false
      this.modalRegister = false
      this.registerForm.email = ''
      this.registerForm.password = ''
      this.registerForm.name = ''
      this.registerForm.phone = ''
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

@media only screen and (max-width: 600px) {
  ::v-deep .modal-dialog {
    align-items: flex-end;
  }
  .modalTitles {
    font-style: normal;
    font-size: 16px;
  }
  .closeBtn {
    border: none;
    display: inline-block;
    padding: 8px 16px;
    vertical-align: middle;
    overflow: hidden;
    text-decoration: none;
    color: inherit;
    background-color: inherit;
    text-align: center;
    cursor: pointer;
    white-space: nowrap;
    font-size: 2rem;
  }
  .top-right {
    position: absolute;
    right: 0;
    top: 0;
  }
}

@media only screen and (min-width: 600px) {
  .closeBtn {
    border: none;
    display: inline-block;
    padding: 8px 16px;
    vertical-align: middle;
    overflow: hidden;
    text-decoration: none;
    color: inherit;
    background-color: inherit;
    text-align: center;
    cursor: pointer;
    white-space: nowrap;
    font-size: 2rem;
  }
  .top-right {
    position: absolute;
    right: 0;
    top: 0;
  }
}

#link {
  color: #ed3237;
}

.modalTitle {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 34px;
}
</style>
