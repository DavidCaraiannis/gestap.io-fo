<template>
<body class="login">
  <div class="container">
    <div class="login-container-wrapper clearfix">
      <ul class="switcher clearfix">
        <li class="first logo active" data-tab="login">
          <a>Login</a>
        </li>
        <li class="second logo" data-tab="sign_up">
          <a>Sign Up</a>
        </li>
      </ul>
      <div class="tab-content">
        <div class="tab-pane active" id="login">
          <div id="loginForm" class="form-horizontal login-form">
            <div class="form-group relative">
              <input class="form-control input-lg" id="login_email" placeholder="Email" required type="email"> <i class="fa fa-user"></i>
            </div>
            <div class="form-group relative">
              <input class="form-control input-lg" id="login_password" placeholder="Password" required type="password"> <i class="fa fa-lock"></i>
            </div>
            <div class="form-group">
              <button class="btn btn-success btn-lg btn-block" @click='login()'>Login</button>
            </div>
          </div>
        </div>
        <div class="tab-pane" id="sign_up">
          <div id="signupForm" class="form-horizontal login-form">
            <div class="form-group relative">
              <input class="form-control input-lg" id="signup_firstname" placeholder="First Name" required type="text"> <i class="fa fa-user"></i>
            </div>
            <div class="form-group relative">
              <input class="form-control input-lg" id="signup_lastname" placeholder="Last Name" required type="text"> <i class="fa fa-user"></i>
            </div>
            <div class="form-group relative">
              <input class="form-control input-lg" id="signup_email" placeholder="E-mail Address" required type="email"> <i class="fa fa-user"></i>
            </div>
            <div class="form-group relative">
              <input class="form-control input-lg" id="signup_password" placeholder="Password" required type="password"> <i class="fa fa-lock"></i>
            </div>
            <div class="form-group">
              <button class="btn btn-success btn-lg btn-block" @click='signup()'>Sign Up</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</body>
</template>

<script>
const axios = require('axios')

export default {
  name: 'Login',
  components: {},
  methods: {
    login: function() {
      var jsonLogin = {
        'email': $('#login_email')[0].value,
        'password': $('#login_password')[0].value
      }
      const url = `http://vps.quentinmodena.fr:2999/users/login`
      axios.post(url, jsonLogin).then(function(response) {
        if (response.data.code == 200) {
          sessionStorage.setItem('email', jsonLogin['email'])
          window.location.href = 'dashboard'
        } else {
          alert('Wrong username or password')
        }
      }).catch(function(response) {
        alert('An error occured. Please try again or contact administrator.')
      })
    },
    signup: function() {
      var jsonSignup = {
        'firstname': $('#signup_firstname')[0].value,
        'lastname': $('#signup_lastname')[0].value,
        'email': $('#signup_email')[0].value,
        'password': $('#signup_password')[0].value,
        'birthday': null,
        'rfid': null,
        'admin': 1
      }
      const url = `http://vps.quentinmodena.fr:2999/users/add`
      axios.post(url, jsonLogin).then(function(response) {
        if (response.data.code == 200) {
          sessionStorage.setItem('email', jsonSignup['email'])
          window.location.href = 'dashboard'
        } else {
          alert('An error occured. Please try again or contact administrator.')
        }
      }).catch(function(response) {
        alert('An error occured. Please try again or contact administrator.')
      })
    }
  }
}

$(document).ready(function() {
  // Switch between login and signup
  $('ul.switcher li').on("click", function() {
    var tab_id = $(this).attr('data-tab')
    $('li').removeClass('active')
    $('div.tab-pane').removeClass('active')

    $(this).addClass('active')
    $("#" + tab_id).addClass('active')
  })
})
</script>

<style scoped lang="scss">
@import url(https://fonts.googleapis.com/css?family=Varela);

body {
    font-family: 'Varela', sans-serif;
    font-size: 14px;
    line-height: 1.5;
    color: #333;
    min-height: 100%;
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
}

label {
    margin-bottom: 0;
}

a {
    color: #e1e1e1;
}

a:focus,
a:hover {
    color: #008080;
}

.checkbox-inline+.checkbox-inline,
.radio-inline+.radio-inline {
    margin-top: 6px;
}

body.login {
    background: rgba(255, 255, 255, 1);
}

.relative {
    position: relative;
}

.switcher {
    margin-bottom: 70px;
}

ul.switcher li {
    list-style-type: none;
    width: 50%;
    position: absolute;
    top: 0;
}

.first {
    left: 0;
}

.second {
    right: 0;
}

.login-container-wrapper {
    max-width: 400px;
    margin: 25% auto 5%;
    padding: 40px;
    box-sizing: border-box;
    background: rgba(57, 89, 116, 0.8);
    position: relative;
    box-shadow: 0 30px 60px -5px #000;
    background-image: url("../assets/login_background.jpg");
    background-size: cover;
    background-blend-mode: saturation;
}

.login-container-wrapper .logo,
.login-container-wrapper .welcome {
    font-size: 16px;
    letter-spacing: 1px;
    color: white;
}

.login-container-wrapper li {
    text-align: center;
    padding: 0 15px;
    background-color: #283443;
    height: 50px;
    line-height: 50px;
    box-shadow: inset 0 -2px 0 0 #ccc;
    cursor: pointer;
}

.login-container-wrapper li a {
    color: #fff;
}

.login-container-wrapper li a:hover {
    color: #ccc;
    text-decoration: none;
}

.login-container-wrapper li a:active,
.login-container-wrapper li a:focus {
    color: #fff;
    text-decoration: none;
}

.login-container-wrapper li.active {
    background-color: transparent;
    box-shadow: none;
}

.login-container-wrapper li.active a {
    border-bottom: 2px solid #fff;
    padding-bottom: 5px;
}

.login input:focus+.fa {
    color: #25a08d;
}

.login-form .form-group {
    margin-right: 0;
    margin-left: 0;
}

.login-form i {
    position: absolute;
    top: 0;
    left: 19px;
    line-height: 52px;
    color: rgba(40, 52, 67, 1);
    z-index: 100;
    font-size: 16px;
}

.login-form .input-lg {
    font-size: 16px;
    height: 52px;
    padding: 10px 25px;
    border-radius: 0;
}

.login input[type="email"],
.login input[type="password"],
.login input[type="text"],
.login input:focus {
    background-color: rgba(40, 52, 67, 0.75);
    border: 0 solid #4a525f;
    color: #eee;
    border-left: 45px solid #93a5ab;
    border-radius: 40px;
}

.login input:focus {
    border-left: 45px solid #eee;
}

input:-webkit-autofill,
select:-webkit-autofill,
textarea:-webkit-autofill {
    background-color: rgba(40, 52, 67, 0.75) !important;
    background-image: none;
    color: rgb(0, 0, 0);
    border-color: #FAFFBD;
}

.login .checkbox a,
.login .checkbox label {
    color: #ddd;
    vertical-align: top;
}

input[type="checkbox"]:checked+label::before,
.checkbox-success input[type="radio"]:checked+label::before {
    background-color: #25a08d !important;
}

.btn-success {
    background-color: #25a08d;
    background-image: none;
    padding: 8px 50px;
    margin-top: 20px;
    border-radius: 40px;
    border: 1px solid #25a08d;
    -webkit-transition: all ease 0.8s;
    -moz-transition: all ease 0.8s;
    transition: all ease 0.8s;
}

.btn-success.active,
.btn-success.active:hover,
.btn-success:active,
.btn-success:active:focus,
.btn-success:active:hover,
.btn-success:focus,
.btn-success:hover {
    background-color: #25a08d;
    border-color: #25a08d;
    box-shadow: 0 5px 35px -5px #25a08d;
    text-shadow: 0 0 8px #fff;
    color: #FFF;
    outline: none;
}
</style>
