<template>
  <div class="view2">
    <h1>Update Profile Picture</h1>
    <p>
      We wanna know you more!
    </p>
    <form class="form-area">
      <div class="upload-up-area" :class="{draging:onDragover}" @drop="drop($event)" @dragover="dragover($event)" @dragleave="dragleave($event)">
          <i class="fas fa-images"></i>
          <input type="file" id="files" multiple @change="drop"/>
          <div class="txt-area">          
            <label for="files">UPLOAD UP TO 3 PHOTOS</label>
            <label for="files">MAXIMUM SIZE: 150*150px</label>
          </div>         
      </div>
      
      <input id="alarmButton" type="button" v-show="isOverSizeFull" value="ONE FILE IS OVER THE MAXIMUM SIZE">
      
      <div class="previewContainer">
        <div class="previewBox" v-for="item in [0,1,2]" :key="item"> 
          <img :id="'preview'+item" src="http://via.placeholder.com/140x140">
          <div class="previewRemove" @click="removePreview(item)"><i class="fas fa-trash-alt"></i></div>
        </div>          
      </div>      
      <input class="button" type="button" value="SUBMIT & NEXT" :disabled="formError" @click="send">
    </form>
  </div>
</template>

<script>
export default {
  name: "view2",
  data: function() {
    return {
      indexOfImage: 0,
      isOverSize: [false, false, false],
      onDragover: false
    };
  },
  computed: {
    formError: function() {
      return this.indexOfImage === 0 || this.isOverSizeFull;
    },
    isOverSizeFull: function() {
      for (let i = 0; i < this.isOverSize.length; i++) {
        if (this.isOverSize[i]) {
          return true;
        }
      }
      return false;
    }
  },
  methods: {
    removePreview: function(i) {
      this.$set(this.isOverSize, i, false);
      document.querySelector("#preview" + i).src =
        "http://via.placeholder.com/140x140";
    },
    send: function() {
      this.$emit("goNext");
    },
    drop: function(event) {
      let that = this;
      for (let i = 0; i < 3; i++) {
        this.removePreview(i);
      }
      this.indexOfImage = 0;
      this.onDragover = false;
      event.stopPropagation();
      event.preventDefault();

      let files;
      let eventType = event.type;
      //用按的 change 用拖曳的 drop
      if (eventType === "change") {
        files = event.target.files; // FileList object
      } else if (eventType === "drop") {
        files = event.dataTransfer.files; // FileList object
      }

      for (var i = 0, f; (f = files[i]); i++) {
        if (!f.type.match("image.*")) {
          // Only process image files.
          continue;
        }

        //get preview
        var reader = new FileReader();
        reader.onload = (function(theFile) {
          return function(e) {
            document.querySelector("#preview" + that.indexOfImage).src =
              e.target.result;
            that.indexOfImage++;
            if (that.indexOfImage === 3) {
              that.indexOfImage = 0;
            }
          };
        })(f);
        reader.readAsDataURL(f);

        //get size
        let img = new Image();
        var _URL = window.URL || window.webkitURL;
        img.attributes.imgIndex = i;
        img.src = _URL.createObjectURL(f);
        img.onload = function(e) {
          const w = this.width;
          const h = this.height;
          const imgIndex = this.attributes.imgIndex;
          that.$set(that.isOverSize, imgIndex, w > 150 && h > 150);
        };
      }
    },
    dragover: function(event) {
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

.upload-up-area {
  border: 2px solid #000;
  border-radius: 8px;
}
.draging {
  border: 2px dotted #f5a623;
  border-radius: 8px;
}
.upload-up-area i {
  font-size: 45px;
  width: 58px;
  height: 45px;
  margin: 48px 20px 47px 69px;
  float: left;
}
.txt-area {
  margin: 46px 78px 46px 20px;
}
input[type="file"] {
  display: none;
}
.txt-area label {
  display: block;
  font-size: 20px;
  color: #9b9b9b;
  line-height: 24px;
}
.previewContainer {
  margin-top: 24px;
  text-align: center;
}
.previewBox {
  display: inline-block;
  margin: 0px 10px;
  cursor: pointer;
}
.previewRemove {
  position: relative;
  background: #0275d8;
  border-radius: 8px;
  height: 40px;
  bottom: 40px;
  font-size: 20px;
  line-height: 40px;
  box-sizing: border-box;
  opacity: 0;
  color: #fff;
}

.previewBox img {
  box-sizing: border-box;
  height: 140px;
  width: 140px;
  margin: 1%;
  border-radius: 8px;
}
.previewBox:hover {
  opacity: 0.8;
}
.previewBox:hover .previewRemove {
  opacity: 1;
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
