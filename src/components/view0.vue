<template>
  <div class="view0">
    <pre>::view0::</pre>
    <h1>Create Account</h1>
    <p>
      Glad to see you here!
    </p>
    <form class="form-area">
      <div class="form-group">
        <label>Account</label>
        <input id="input-email" type="email" placeholder="example@eamil.com" v-model="mail"/>
        <div class="alarm" v-show="mailError">INVALID EMAIL</div>
      </div>
      <div class="form-group">
        <label>Password</label>
        <input id="input-password" type="password" placeholder="password" v-model="password"/>
        <div class="alarm" v-show="passwordError">MINIMUM 8 CHARACTERS</div>
      </div>
      <div class="form-group">
        <label>Comfirm Password</label>
        <input id="input-password2" type="password" placeholder="password" v-model="password2"/>
        <div class="alarm" v-show="password2Error">NOT MATCH</div>
      </div>
      <input class="button" type="button" value="SUBMIT & NEXT" :disabled="formError" @click="send">
    </form>
  </div>
</template>

<script>
export default {
  name: "view0",
  props: {
    msg: String
  },
  data: function() {
    return {
      mail: "",
      password: "",
      password2: ""
    };
  },
  computed: {
    formError: function() {
      let error = this.mailError || this.passwordError || this.password2Error;
      return error;
    },
    mailError: function() {
      let ret = true;
      let v = this.mail;
      if (v !== "" && v.indexOf("@") >= 0) {
        ret = false;
      }
      return ret;
    },
    passwordError: function() {
      let ret = true;
      let v = this.password;
      if (v.length >= 8) {
        ret = false;
      }
      return ret;
    },
    password2Error: function() {
      let ret = true;
      let v = this.password;
      let v2 = this.password2;
      if (v !== "" && v2 !== "" && v === v2) {
        ret = false;
      }
      return ret;
    }
  },
  methods: {
    send: function() {
      this.$emit("goNext");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.view0 h1 {
  margin-top: 54px;
  font-family: "Roboto";
  font-size: 48px;
  line-height: 0;
}
.view0 p {
  font-family: "Roboto";
  font-size: 24px;
}
.alarm {
  display: inline;
  background-color: #f5a623;
}
.form-area {
  text-align: start;
  width: 30%;
  margin: auto;
}
.form-group label {
  display: block;
  font-size: 20px;
  padding: 8px 0;
}
#input-email,
#input-password,
#input-password2 {
  width: 100%;
  height: 52px;
  border-radius: 8px;
  border: 2px solid #000;
}
input::placeholder {
  font-size: 20px;
  box-sizing: border-box;
  padding: 12px 20px;
}
</style>
