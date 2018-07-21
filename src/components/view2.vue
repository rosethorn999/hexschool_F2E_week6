<template>
  <div class="view2">
    <pre>::view2::</pre>
    <h1>Update Profile Picture</h1>
    <p>
      We wanna know you more!
    </p>
    <form>
      <div>
          <img src="http://via.placeholder.com/150x150">
          <p>UPLOAD UP TO 3 PHOTOS</p>
          <span>MAXIMUM SIZE: 150*150px</span>
      </div>
      <div>
          <img src="http://via.placeholder.com/50x50">
          <img src="http://via.placeholder.com/50x50">
          <img src="http://via.placeholder.com/50x50">
      </div>
      <input type="button" value="ONE FILE IS OVER THE MAXIMUM SIZE">
    </form>
  </div>
</template>

<script>
export default {
  name: "view2",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
