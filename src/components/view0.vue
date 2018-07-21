<template>
  <div class="view0">
    <pre>::view0::</pre>
    <h1>Create Account</h1>
    <p>
      Glad to see you here!
    </p>
    <form>
      <div class="form-group">
        <label>Account</label>
        <input type="email" placeholder="example@eamil.com"/>
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" placeholder="password"/>
      </div>
      <div class="form-group">
        <label>Comfirm Password</label>
        <input type="password" placeholder="password"/>
      </div>
      <input type="button" value="SUBMIT & NEXT">
    </form>
  </div>
</template>

<script>
export default {
  name: "view0",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
