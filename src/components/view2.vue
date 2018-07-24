<template>
  <div class="view2">
    <pre>::view2::</pre>
    <h1>Update Profile Picture</h1>
    <p>
      We wanna know you more!
    </p>
    <form class="form-area">
      <div class="upload-up-area">
          <img src="http://via.placeholder.com/150x150">
          <div class="txt-area">          
            <span>UPLOAD UP TO 3 PHOTOS</span>
            <span>MAXIMUM SIZE: 150*150px</span>
          </div>
          <!-- <img src="http://via.placeholder.com/50x50">
          <img src="http://via.placeholder.com/50x50">
          <img src="http://via.placeholder.com/50x50"> -->
      </div>

      <input id="button"  type="button" value="ONE FILE IS OVER THE MAXIMUM SIZE">
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
.view2 h1 {
  margin-top: 54px;
  font-family: "Roboto";
  font-size: 48px;
  line-height: 0;
}
.view2 p {
  font-family: "Roboto";
  font-size: 24px;
}
.form-area {
  text-align: start;
  width: 30%;
  margin: auto;
}
.upload-up-area {
  border: 2px solid #000;
  border-radius: 8px;
}
.upload-up-area img {
  width: 58px;
  height: 45px;
  margin: 48px 20px 47px 69px;
  float: left;
}
.txt-area {
  margin: 46px 78px 46px 20px;
}
.txt-area span {
  display: block;
  font-size: 20px;
  color: #9b9b9b;
  line-height: 24px;
}
#button {
  background: #bde0fd;
  border: 0;
  width: 100%;
  height: 52px;
  border-radius: 8px;
  margin-top: 40px;
  font-family: "Roboto" !important;
  font-size: 20px;
  color: white;
  cursor: pointer;
}
</style>
