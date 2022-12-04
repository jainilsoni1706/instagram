<template>
  <div class="body" :style="{backgroundColor: theme == 'dark' ? 'black' : 'white'}">

    <div class="select-language">
      English (United States)
    </div>

    <div class="container">
      <center>
        <img class="logo-text" :src="logo" alt="">
      </center>
      
      <input type="text" id="email" class="form-control" placeholder="Phone number, email or username">
      <input type="password" id="password" class="form-control" placeholder="Password">

      <div class="login-button">
        <button class="btn btn-primary">Log in</button>
      </div>

    </div>

    <div class="signup-option">
      Don't have an account? <span>Sign up.</span>
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

    isEmpty : function() 
    {

      return true;

    }
  },
  mounted() {

    this.modeDetector();
    alert(this.isEmpty());
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

.signup-option > span {
  color: darkblue;
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

</style>
  
 