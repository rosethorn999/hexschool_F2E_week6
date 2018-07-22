<template>
  <div class="view4">
    <pre>::view4::</pre>
    <h1>Congratulations</h1>
    <p>
      Now you're one of us!
    </p>
    <form>
      <div><img src="../assets/facebook.png"></div>
      <div class="redirected-link"><a href="#" ><i>Redirected to homepage after 5 secconds...</i></a></div>
      
    </form>
  </div>
</template>

<script>
export default {
  name: "view4",
  props: {
    msg: String
  },
  mounted: function() {
    setTimeout(() => {
      this.$emit("goNext");
    }, 5000);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.view4 h1 {
  font-size: 48px;
  line-height: 57px;
}
.view4 p {
  font-size: 24px;
  line-height: 28px;
}
img {
  border-radius: 50%;
}
.redirected-link {
  font-family: Roboto-Italic;
  font-size: 20px;
  color: #0275d8;
  margin-top: 25px;
}
</style>
