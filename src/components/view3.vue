<template>
  <div class="view3">
    <pre>::view3::</pre>
    <h1>Payment Method</h1>
    <p>
      Add your credit cared information!
    </p>
    <form>
      <div class="form-group">
        <label>Card Number</label>
        <input type="text"  v-model="cardNumber" placeholder="1234567890123456"/>
        <label>{{binCode}}</label>
        <div class="alarm" v-show="cardNumberError">REQUIRED FIELD</div>
      </div>
      <div class="form-group">
        <label>Cardholder Name</label>
        <input type="text" v-model="cardHolder" placeholder="Elon Musk"/>
        <div class="alarm" v-show="cardHolderError">REQUIRED FIELD</div>
      </div>
      <div class="form-group">
        <label>Bank Name</label>
        <input type="text" v-model="bankName"  placeholder="City Group"/>
         <div class="alarm" v-show="bankNameError">REQUIRED FIELD</div>
      </div>
      <div class="form-group">
        <label>CVV</label>
        <input type="text" v-model="CVV" placeholder="123"/>
        <div class="alarm" v-show="CVVError">MUST BE 3 CHARACTERS</div>
      </div>
      <div class="form-group">
        <label>Expire Date</label>
        <select>
            <option v-for="(MM,index) in 12" :key="index">{{MM}}</option>
        </select> <select>
            <option v-for="(DD,index) in 31" :key="index">{{DD}}</option>
        </select>
      </div>
      <input type="button" value="DONE" :disabled="formError" @click="send">
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
      MM: 1,
      YY: 1
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
  display: inline;
  background-color: #f5a623;
}
</style>
