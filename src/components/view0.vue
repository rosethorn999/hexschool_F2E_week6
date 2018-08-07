<template>
  <div class="view0">
    <h1>Create Account</h1>
    <p>
      Glad to see you here!
    </p>
    <form class="form-area">
      <div class="form-group">
        <label>Account</label>
        <div :class="{emailDiv:mailError}">
          <input id="input-email" type="email" placeholder="example@eamil.com" v-model="mail"/>
        </div>
      </div>
      <div class="form-group">
        <label>Password</label>
        <div :class="{passwordDiv:passwordError}">
          <input id="input-password" type="password" placeholder="password" v-model="password"/>
        </div>
      </div>
      <div class="form-group">
        <label>Comfirm Password</label>
        <div :class="{passwordDiv:password2Error}">
          <input id="input-password2" type="password" placeholder="password" v-model="password2"/>
        </div>
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
.emailDiv,
.passwordDiv,
.password2Div {
  position: relative;
}

.emailDiv::before,
.passwordDiv::before,
.password2Div::before {
  font-family: "Font Awesome 5 Free";
  content: "\f556";
  display: inline-block;
  vertical-align: middle;
  position: absolute;
  font-size: 22px;
  z-index: 10;
  line-height: 56px;
  right: 20px;
  color: #f5a623;
}
.emailDiv::after {
  content: "INVALID EMAIL";
  position: absolute;
  background-color: #f5a623;
  border-radius: 5px;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 5px;
  height: 18px;
  right: -130px;
}
.passwordDiv::after {
  content: "MINIMUM 8 CHARACTERS";
  position: absolute;
  background-color: #f5a623;
  border-radius: 5px;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 5px;
  height: 18px;
  right: -210px;
}
.password2Div::after {
  content: "NOT MATCH";
  position: absolute;
  background-color: #f5a623;
  border-radius: 5px;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 5px;
  height: 18px;
  right: -110px;
}
</style>
