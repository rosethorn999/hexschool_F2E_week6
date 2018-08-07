<template>
  <div class="view3">
    <h1>Payment Method</h1>
    <p>
      Add your credit cared information!
    </p>
    <form class="form-area">
      <div class="form-group" id="form-group-CardNum">
        <label>Card Number ({{binCode}})</label>
        <div :class="{cardNumberDiv:cardNumberError}">
          <input type="text" v-model="cardNumber" placeholder="1234567890123456"/>
        </div>
      </div>
      <div class="form-group" id="form-group-Cardholder">
        <label>Cardholder Name</label>
        <div>
          <input type="text" v-model="cardHolder" placeholder="Elon Musk"/>
        </div>
      </div>
      <div class="form-group" id="form-group-Bank">
        <label>Bank Name</label>
        <div>
          <input type="text" v-model="bankName" placeholder="City Group"/>
        </div>
      </div>
      <div class="form-group" id="form-group-CVV">
        <label>CVV</label>
        <div>
          <input type="text" v-model="CVV" placeholder="123"/>
        </div>
      </div>
      <div class="form-group" id="form-group-Date">
        <label>Expire Date</label>
        <select v-model="eMM" id="form-group-Date-MM">
            <option v-for="(MM,index) in MMs" :key="index">{{MM}}</option>
        </select>
        <select v-model="eYY" id="form-group-Date-YY">
            <option v-for="(YY,index) in YYs" :key="index">{{YY}}</option>
        </select>
      </div>
      <input class="button" type="button" value="DONE" :disabled="formError" @click="send">
    </form>
  </div>
</template>

<script>
export default {
  name: "view3",
  props: {
    msg: String
  },
  data: function() {
    return {
      cardNumber: "",
      cardHolder: "",
      bankName: "",
      CVV: "",
      eMM: "01",
      eYY: "18",
      MMs: [
        "01",
        "02",
        "03",
        "04",
        "05",
        "06",
        "07",
        "08",
        "09",
        "10",
        "11",
        "12"
      ],
      YYs: ["18", "19", "20", "21", "22", "23", "24", "25"]
    };
  },
  computed: {
    binCode: function() {
      let ret = "OTHER";
      let bin = this.cardNumber;
      // VISA 4開始
      // MC 51~55開始
      // AE 34 37開始
      // 銀聯 62
      // JCB 3528開始
      let first2 = Number(bin.substring(0, 2));
      if (first2 === 35) {
        ret = "JCB";
      } else if (first2 === 34 || first2 === 37) {
        ret = "AE";
      } else if (first2 >= 40 && first2 <= 49) {
        ret = "VISA";
      } else if (first2 >= 52 && first2 <= 55) {
        ret = "MC";
      }
      return ret;
    },
    formError: function() {
      let error = this.cardNumberError;
      return error;
    },
    cardNumberError: function() {
      let ret = true;
      let v = this.cardNumber;
      if (v !== "") {
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
.view3 h1 {
  margin-top: 54px;
  font-family: "Roboto";
  font-size: 48px;
  line-height: 0;
}
.view3 p {
  font-family: "Roboto";
  font-size: 24px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-size: 20px;
  color: #000000;
  letter-spacing: 0;
}
.form-group input,
.form-group select {
  background: #ffffff;
  border: 2px solid #000000;
  border-radius: 8px;
  padding: 12px 20px 16px;
  font-size: 20px;
  color: #999999;
  letter-spacing: 0;
  text-align: left;
  line-height: 24px;
  box-sizing: border-box;
}
#form-group-CardNum {
  box-sizing: border-box;
}
#form-group-CardNum input {
  width: 100%;
}

#form-group-Cardholder {
  box-sizing: border-box;
  display: inline-block;
  width: 45%;
  margin-right: 5%;
  margin-top: 3%;
}
#form-group-Bank {
  box-sizing: border-box;
  display: inline-block;
  width: 50%;
  margin-top: 3%;
}
#form-group-Cardholder input {
  /*margin-right: 5px;*/
  width: 100%;
}
#form-group-Bank input {
  /*margin-left: 5px;*/
  width: 100%;
}
#form-group-CVV {
  float: left;
  width: 32%;
  margin-right: 6px;
  margin-top: 3%;
}
#form-group-CVV input {
  width: 100%;
}
#form-group-Date {
  margin-top: 3%;
}
#form-group-Date select {
  width: 33%;
}
.cardNumberDiv {
  position: relative;
}
.cardNumberDiv::before {
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
.cardNumberDiv::after {
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
</style>
