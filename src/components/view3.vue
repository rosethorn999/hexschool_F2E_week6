<template>
  <div class="view3">
    <h1>Payment Method</h1>
    <p>
      Add your credit cared information!
    </p>
    <form class="form-area">
      <div class="form-group" id="form-group-CardNum">
        <label>Card Number</label>
        <input type="text"  v-model="cardNumber" placeholder="1234567890123456"/>
        <label>{{binCode}}</label>
        <div class="alarm" v-show="cardNumberError">REQUIRED FIELD</div>
      </div>
      <div class="form-group" id="form-group-Cardholder">
        <label>Cardholder Name</label>
        <input type="text" v-model="cardHolder" placeholder="Elon Musk"/>
        <div class="alarm" v-show="cardHolderError">REQUIRED FIELD</div>
      </div>
      <div class="form-group" id="form-group-Bank">
        <label>Bank Name</label>
        <input type="text" v-model="bankName"  placeholder="City Group"/>
         <div class="alarm" v-show="bankNameError">REQUIRED FIELD</div>
      </div>
      <div class="form-group" id="form-group-CVV">
        <label>CVV</label>
        <input type="text" v-model="CVV" placeholder="123"/>
        <div class="alarm" v-show="CVVError">MUST BE 3 CHARACTERS</div>
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
      let error =
        this.cardNumberError ||
        this.cardHolderError ||
        this.bankNameError ||
        this.CVVError;
      return error;
    },
    cardNumberError: function() {
      let ret = true;
      let v = this.cardNumber;
      if (v !== "") {
        ret = false;
      }
      return ret;
    },
    cardHolderError: function() {
      let ret = true;
      let v = this.cardHolder;
      if (v !== "") {
        ret = false;
      }
      return ret;
    },
    bankNameError: function() {
      let ret = true;
      let v = this.bankName;
      if (v !== "") {
        ret = false;
      }
      return ret;
    },
    CVVError: function() {
      let ret = true;
      let v = this.CVV;
      if (v.length === 3) {
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
.alarm {
  display: block;
  background-color: #f5a623;
  width: 125px;
}

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

.form-area {
  text-align: start;
  width: 30%;
  margin: auto;
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
}
#form-group-Bank {
  box-sizing: border-box;
  display: inline-block;
  width: 50%;
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
}
#form-group-CVV input {
  width: 100%;
  -webkit-appearance:none;
}
#form-group-Date select {
  width: 33%;
  -webkit-appearance:none;
}
</style>
