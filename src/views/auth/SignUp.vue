<template>
  <div class="container-fluid d-flex justify-content-center align-items-center">
    <main class=" box-auth d-flex flex-column align-items-center">
      <!-- Title Login -->
      <div class="d-flex w-100 justify-content-center align-items-center position-relative">
        <div class=" align-self-start position-absolute img">
          <img src="../../assets/back.svg" alt="back" @click="goLogin" height="26px">
        </div>
        <h1>Register</h1>
      </div>
      <div class="space"></div>
      <h2 class=" align-self-start">Let’s create your account!</h2>
      <div class="space"></div>
      <!-- Form -->
      <form @submit.prevent="signup" class=" d-flex flex-column">
        <!-- Full Name -->
        <label for="name" class=" align-self-start">Name</label>
        <input :class="this.errorName === 1 ? 'bottom-red': '' " @input="checkName" type="text" id="name" v-model="fullName" maxlength="64" placeholder="Enter your full name, ex: John Doe" required>
        <div class=" w-100 mb-1" v-if="this.errorName === 1"></div>
        <h6 class=" align-self-start" v-if="this.errorName === 1">Do you have a name? Please input here</h6>
        <div class="space"></div>
        <!-- Email -->
        <label for="email" class=" align-self-start">Email</label>
        <input :class="this.errorEmail === 1 ? 'bottom-red': '' " @input="checkEmail" type="email" id="email" v-model="email" maxlength="64" placeholder="Enter your email, ex: telegrum@gmail.com" required>
        <div class=" w-100 mb-1" v-if="this.errorEmail === 1"></div>
        <h6 class=" align-self-start" v-if="this.errorEmail === 1">Email format is wrong!</h6>
        <div class="space"></div>
        <!-- Password -->
        <label for="password" class=" align-self-start">Password</label>
        <input :class="this.errorPass === 1 ? 'bottom-red': '' " @input="checkPass" type="password" id="password" v-model="password" minlength="8" maxlength="64" placeholder="Enter your password, min 8 char" required>
        <div class=" w-100 mb-1" v-if="this.errorPass === 1"></div>
        <h6 class=" align-self-start" v-if="this.errorPass === 1">Password must be 8 character</h6>
        <div class="space"></div>
        <!-- Button Register -->
        <BtnAuth title="Register"/>
        <div class="space"></div>
      </form>
      <!-- Text Muted -->
      <div class="d-flex w-100 align-items-center">
        <div class="line-muted flex-grow-1"></div>
        <h4>Register with</h4>
        <div class="line-muted flex-grow-1"></div>
      </div>
      <div class="space"></div>
      <!-- Button Google -->
      <BtnGoogle/>
    </main>
  </div>
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'
import BtnAuth from '../../components/auth/base/BtnAuth'
import BtnGoogle from '../../components/auth/base/BtnGoogle'

export default {
  title: 'Sign Up',
  name: 'SignUp',
  components: {
    BtnAuth,
    BtnGoogle
  },
  data () {
    return {
      email: '',
      password: '',
      fullName: '',
      errorEmail: 0,
      errorPass: 0,
      errorName: 0
    }
  },
  methods: {
    checkEmail () {
      if (!this.email.includes('@')) {
        this.errorEmail = 1
      } else {
        this.errorEmail = 0
      }
    },
    checkPass () {
      if (this.password.length < 8) {
        this.errorPass = 1
      } else {
        this.errorPass = 0
      }
    },
    checkName () {
      if (this.fullName.length === 0) {
        this.errorName = 1
      } else {
        this.errorName = 0
      }
    },
    signup () {
      const email = this.email
      const password = this.password
      const fullName = this.fullName
      const data = { email, password, fullName }
      console.log(data)
      axios.post(`${process.env.VUE_APP_BASE_URL}auth/signup`, data)
        .then((res) => {
          console.log(res.data)
          Swal.fire('Success Register', 'Let\'s Go Login', 'success')
          this.$router.push('/login')
        })
        .catch((err) => {
          console.log(err.response.data.err)
          Swal.fire('Failed Register', err.response.data.err, 'error')
        })
    },
    goLogin () {
      this.$router.push('/login')
    }
  }
}
</script>

<style lang="scss" scoped>

.container-fluid {
  padding: 100px 0;
  background: #F6F6F6;
}

.space {
  width: 100%;
  height: 35px;
}

.img {
  left: 0;
  top: 0;
}

.img:hover {
  opacity: .8;
}

img {
  cursor: pointer;
}

h1 {
  font-family: Rubik;
  font-style: normal;
  font-weight: 500;
  font-size: 22px;
  line-height: 26px;
  text-align: center;
  letter-spacing: -0.165px;
  color: #7E98DF;
}

h2 {
  font-family: Rubik;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 17px;
  color: #232323;
}

h3 {
  font-family: Rubik;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 19px;
  text-align: right;
  color: #7E98DF;
  cursor: pointer
}

h3:hover {
  opacity: .8;
}

h4 {
  font-family: Rubik;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 19px;
  color: #848484;
  margin: 0 40px;
  width: fit-content;
}

h5 {
  font-family: Rubik;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 17px;
  color: #313131;
  span {
    color: #7E98DF;
    cursor: pointer;
  }
  span:hover {
    opacity: .8;
  }
}

.bottom-red {
  border-bottom: 1px solid #FF5B37;
}

h6 {
  text-align: center;
  font-family: Rubik;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 17px;
  color: #FF5B37;
}

.line-muted {
  height: 1px;
  background-color: #848484;
}

form {
  width: 100%;
}

label {
  font-family: Rubik;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 17px;
  color: #848484;
  opacity: 0.75;
}

input {
  font-family: Rubik;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 19px;
  color: #232323;
  border-bottom: 1px solid #adadad;
  padding: 15px 0;
  width: 100%;
}

input::placeholder {
  color: rgba(35, 35, 35, 0.2);
}

@media (min-height: 910px) {
  .container-fluid {
    height: 100vh;
  }
}

@media (max-width: 575px) {
  .container-fluid {
    padding: 40px 20px;
  }
  .box-auth {
    padding: 40px 30px;
  }
}

</style>
