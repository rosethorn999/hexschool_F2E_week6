<template>
  <div class="view2">
    <pre>::view2::</pre>
    <h1>Update Profile Picture</h1>
    <p>
      We wanna know you more!
    </p>
    <form class="form-area">
      <div class="upload-up-area" :class="{draging:onDragover}" @drop="drop($event)" @dragover="allowDrop($event)" @dragleave="dragleave($event)">
          <img src="http://via.placeholder.com/150x150">
          <div class="txt-area">          
            <span>UPLOAD UP TO 3 PHOTOS</span>
            <span>MAXIMUM SIZE: 150*150px</span>
          </div>         
      </div>

      <input id="alarmButton" type="button" v-show="isOverSize" value="ONE FILE IS OVER THE MAXIMUM SIZE">
      
      <div class="preview">
        <img id="preview0" src="http://via.placeholder.com/140x140">
        <img id="preview1" src="http://via.placeholder.com/140x140">
        <img id="preview2" src="http://via.placeholder.com/140x140">
      </div>

      <input class="button" type="button" value="SUBMIT & NEXT" :disabled="formError" @click="send">
    </form>
  </div>
</template>

<script>
export default {
  name: "view2",
  props: {
    msg: String
  },
  data: function() {
    return {
      indexOfImage: 0,
      isOverSize: false,
      onDragover: false
    };
  },
  computed: {
    formError: function() {
      return this.indexOfImage === 0 || this.isOverSize;
    }
  },
  methods: {
    send: function() {
      this.$emit("goNext");
    },
    drop: function(event) {
      this.onDragover = false;
      this.indexOfImage = 0;
      this.isOverSize = false;
      let that = this;
      event.preventDefault();
      var dt = event.dataTransfer;
      var files = dt.files;
      for (var i = 0; i < files.length; i++) {
        var file = files[i];
        var reader = new FileReader();
        reader.readAsDataURL(file);
        reader.addEventListener(
          "loadend",
          function(e) {
            var bin = this.result;
            var img = document.createElement("img");
            img.file = file;
            img.src = bin;
            // console.log(that.isOverSize);
            if (that.isOverSize === false) {
              let tooBig = img.naturalWidth > 150 || img.naturalHeight > 150;
              console.log(img.width + "," + img.height);
              if (tooBig) {
                that.isOverSize = tooBig;
              }
            }
            // document.querySelector(".preview").appendChild(img);
            document.querySelector("#preview" + that.indexOfImage).src = bin;
            that.indexOfImage++;
          },
          false
        );
      }
    },
    allowDrop: function(event) {
      this.onDragover = true;
      event.preventDefault();
    },
    dragleave: function() {
      this.onDragover = false;
      event.preventDefault();
    }
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
.draging {
  border: 2px dotted #f5a623;
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
.preview {
  margin-top: 24px;
  text-align: center;
}
.preview img {
  box-sizing: border-box;
  height: 140px;
  width: 140px;
  margin: 1%;
  border-radius: 8px;
}
.preview img:hover {
  opacity: 0.8;
}
#alarmButton {
  background: #f5a623;
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
