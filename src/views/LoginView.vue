<template>
  <div class="body" :style="{backgroundColor: theme == 'dark' ? 'black' : 'white'}">

    <div class="select-language">
      English (United States)
    </div>

    <div class="container">
      <center>
        <img class="logo-text" :src="logo" alt="">
      </center>
      
      <input type="text" id="email" class="form-control" v-model="email" placeholder="Phone number, email or username" :style="{color: theme == 'dark' ? 'white' : 'black'}" autocomplete="off">
      <div class="password-box">
        <input type="password" id="password" class="form-control" v-model="password" placeholder="Password" v-on:keypress="valueChecker()" :style="{color: theme == 'dark' ? 'white' : 'black'}" autocomplete="off">
        <span id="hide" :style="{color: theme == 'dark' ? 'white' : 'black'}"  v-on:click="togglePassword()" >HIDE</span>
        <span id="show" :style="{color: theme == 'dark' ? 'white' : 'black'}"  v-on:click="togglePassword()" >SHOW</span>
      </div>

      <div class="login-button">
        <button v-on:click="login" class="btn btn-primary login" id="login">Log in</button>
      </div>

      <div class="forgot-password">
        Forgot your login details? <span :style="{color: theme == 'dark' ? '#afdcf9' : 'darkblue'}" > Get help logging in.</span> 
      </div>  

      <div class="or-div">
        <div class="line"></div>
        <div class="text">OR</div>
        <div class="line"></div>
      </div>

      <div class="login-button">
        <button class="btn btn-primary"> <img src="<%= BASE_URL %>../../assets/icon/facebook.png" alt=""> Continue with Facebook</button>
      </div>

    </div>

    <div class="signup-option">
      Don't have an account? <span  :style="{color: theme == 'dark' ? '#afdcf9' : 'darkblue'}" >Sign up.</span>
    </div>

    <div class="error-box" v-if="cError">
        <h3 class="error-heading"> {{headingMessage}}</h3>
        <p class="error-message-one"> {{messageOne}}</p>
        <p class="error-message-two"> {{messageTwo}}</p>
        <div v-on:click="cError=false">OK</div>
    </div>

  </div>
</template>
  
<script lang="ts">
import { defineComponent } from 'vue';
import { useRouter } from 'vue-router';

export default defineComponent({
  name: 'LoginView',
  data : function(){
    return {
      mode : true,
      theme : "",
      logo : "",
      passwordPermission : false,
      email : null,
      password : null,
      cError : false,
      loginFail : 0,
      headingMessage : "Incorrect password",
      messageOne : "The Password you entered is",
      messageTwo : "incorrect. Please try again.",
    }
  },
  setup() {
    const router = useRouter();
    return { router };
  },
  methods : {
    modeDetector : function()
    {
      this.mode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;

      if (this.mode === true) {
        this.theme = "dark";
        this.logo = "<%= BASE_URL %>../../assets/icon/textdark.png"; 

      } else {
        this.theme = "light";
        this.logo = "textlight.png";
        this.logo = "<%= BASE_URL %>../../assets/icon/textlight.png";
      }
    },

    togglePassword : function()
    {
      if (this.passwordPermission === false) {
        this.$el.querySelector("#password").type = "text";
        this.$el.querySelector("#hide").style.display = "block";
        this.$el.querySelector("#show").style.display = "none";
        this.passwordPermission = true;
      } else {
        this.$el.querySelector("#password").type = "password";
        this.$el.querySelector("#hide").style.display = "none";
        this.$el.querySelector("#show").style.display = "block";
        this.passwordPermission = false;
      }
    },

    valueChecker : function()
    {
      if (this.email !== null) {
        if (this.password !== null) {
          this.$el.querySelector("#login").disabled = false;
          this.$el.querySelector("#login").style.backgroundColor = "#0095f6!important";
        } else {
          this.$el.querySelector("#login").disabled = true;
          this.$el.querySelector("#login").style.backgroundColor = "#a1c8e2!important";
          console.log("true");
        }
      }
    },

    login : function()
    {
      if (this.email !== null && this.password !== null) {
        if (this.loginFail > 5) {
            this.headingMessage = "Too many attempts";
            this.messageOne = "You've tried too login many times.";
            this.messageTwo = "Please try again later.";
        this.cError = true;
      } else {
        if (this.email == 'vue' && this.password == 'vue') {
            this.headingMessage = "Issue Detected";
            this.messageOne = "some issue detected while.";
            this.messageTwo = "logging in to instagram.";          
          this.cError = true;
        } else {
          this.cError = true;
          this.loginFail++;
        }
        }
    } else {
      this.headingMessage = "Please enter Credentials";
      this.messageOne = "Please enter your login";
      this.messageTwo = " credentials to login.";
      this.cError = true;
    }
    }

  },
  mounted() {

    this.modeDetector();
    this.$el.querySelector("#hide").style.display = "none";
  }
});
</script>


<style scoped>

.body {
  background-color: #ffffff;
  color: black;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
  }


.select-language {
  position: fixed;
  top: 0;
  width: 100%;
  text-align: center;
  padding: 10px 0px;
  color: gray;
  font-size: 14px;
  font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}

.signup-option {
  position: fixed;
  bottom: 0;
  width: 100%;
  text-align: center;
  padding-top: 15px;
  padding-bottom: 15px;
  border-top: 1px solid #80808038;
  color: gray;
  font-size: 12px;
}

.forgot-password {
  width: 100%;
  text-align: center;
  padding-top: 7px;
  padding-bottom: 15px;
  color: gray;
  font-size: 12px;
}

.signup-option > span, .forgot-password > span {
  font-weight: 600;
}

.container {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
}

.logo-text {
  width: 180px;
  height: 65px;
  margin-top: 40%;
  margin-bottom: 20px;
}

.form-control {
  width: 80%;
  margin: 0 auto;
  margin-bottom: 10px;
  padding: 15px 15px;
  border: 1px solid #80808038;
  border-radius: 5px;
  font-size: 14px;
  font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  outline: none;
}

.login-button {
  width: 80%;
  margin: 0 auto;
  margin-top: 10px;
  margin-bottom: 10px;
}

.btn {
  width: 100%;
  padding: 15px 15px;
  border: none;
  border-radius: 5px;
  font-size: 14px;
  font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  outline: none;
  cursor: pointer;
}

.btn-primary {
  background-color: #0095f6;
  color: white;
}

.or-div {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin: 10px 0px;
  width: 100%;
}

.line {
  width: 35%;
  height: 1px;
  background-color: #80808038;
}

.text {
  margin: 0 10px;
  color: gray;
  font-size: 12px;
}

.btn-primary > img {
  width: 15px;
  height: 15px;
  position: relative;
  top: 2px;
  right:4px;
}

#hide , #show {
  font-size:10px;
}

.password-box {
  display: flex;
  flex-direction: column;
  position: relative;
}

.password-box > span {
  position: absolute;
  right: 50px;
  top: 20px;
  cursor: pointer;
}

.error-box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80%;
  text-align: center;
  border-radius: 20px;
  color: black!important;
  padding-bottom: 20px;
  font-size: 12px;
  background-color: white;
}

.error-box > div {
  font-size: 14px;
  border-top: 1px solid #80808038;
  padding-top: 15px;
}

.error-box > h3 {
  font-size: 22px;
  font-weight: 600;
  font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}

.error-box > p {
  font-size: 14px;
  font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}

.error-box > p:nth-child(2) {
  position: relative;
  top: 11px;
}

</style>

  
 