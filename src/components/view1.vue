<template>
  <div class="view1">
    <h1>General Infomation</h1>
    <p>
      Tell us who you are!
    </p>
    <form class="form-area">
      <div class="form-group" id="form-group-name">
        <label class="label-title">Name(optional)</label>
        <input type="text" placeholder="example@eamil.com" v-model="name"/>
      </div>
      <div class="form-group" id="form-group-telphone">
        <label class="label-title">Phone</label>
        <input type="telphone" placeholder="0912345678" v-model="telphone"/>
        <div class="alarm" v-show="telphoneError">NUMBER ONLY</div>
      </div>
      <div class="form-group" id="form-group-birthday">
        <label class="label-title">Birth Date(optional)</label>
        <select class="birthday-yyyy" v-model="YYYY">
            <option v-for="(YYYY,index) in YYYYs" :key="index">{{YYYY}}</option>
        </select>
        <select class="birthday-mm">
            <option v-for="(MM,index) in 12" :key="index">{{MM}}</option>
        </select>
        <select class="birthday-dd">
            <option v-for="(DD,index) in 31" :key="index">{{DD}}</option>
        </select>
      </div>
       <div class="form-group" id="form-group-address">
        <label class="label-title">Address</label>
        <select v-model="city">
            <option v-for="(city,index) in citys" :key="index" :value="index">{{city}}</option>
        </select>
        <select v-model="dist">
            <option v-for="(dist,index) in districts" :key="index" :value="index">{{dist}}</option>
        </select>
        <input type="text" v-model="address" placeholder="detail address"/>
         <div class="alarm" v-show="addressError">REQUIRED FILED</div>
      </div>
      <input class="button" type="button" value="SUBMIT & NEXT" :disabled="formError" @click="send">
    </form>
  </div>
</template>

<script>
export default {
  name: "view1",
  props: {
    msg: String
  },
  data: function() {
    return {
      name: "",
      telphone: "",
      YYYY: "1950",
      city: 0,
      dist: 0,
      address: "",
      counties: []
    };
  },
  mounted: function() {
    const counties = require("../assets/counties.json");
    this.counties = counties;
  },
  computed: {
    formError: function() {
      let error = this.telphoneError || this.addressError;
      return error;
    },
    YYYYs: function() {
      let ret = [];
      for (let i = 1950; i < 2000; i++) {
        ret.push(i);
      }
      return ret;
    },
    telphoneError: function() {
      let ret = true;
      let v = this.telphone;
      var reg = new RegExp(/^\d+$/);
      let vaild = reg.test(v);
      if (v !== "" && vaild) {
        ret = false;
      }
      return ret;
    },
    addressError: function() {
      let ret = true;
      let v = this.address;
      if (v !== "") {
        ret = false;
      }
      return ret;
    },
    citys: function() {
      let ret = [];
      let c = this.counties;
      if (c && c.counties && c.counties.length > 0) {
        ret = c.counties;
      }
      return ret;
    },
    districts: function() {
      let ret = [];
      let c = this.counties;
      let city = this.city;
      if (c && c.districts && c.districts.length > 0) {
        ret = c.districts[city][0];
        this.dist = 0;
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
.view1 h1 {
  margin-top: 54px;
  font-family: "Roboto";
  font-size: 48px;
  line-height: 0;
}
.view1 p {
  font-family: "Roboto";
  font-size: 24px;
}
.form-group {
  margin-bottom: 24px;
}
#form-group-name {
  float: left;
  width: 50%;
}

#form-group-name input,
#form-group-telphone input,
#form-group-address input,
select {
  font-size: 20px;
  color: #999999;
  letter-spacing: 0;
  text-align: left;
  line-height: 24px;
}
#form-group-name input {
  width: 100%;
  background: #ffffff;
  border: 2px solid #000000;
  border-radius: 8px;
  padding: 12px 20px 16px;
  margin-right: 15px;
  box-sizing: border-box;
}
#form-group-telphone {
  float: right;
  width: 50%;
}
#form-group-telphone input {
  width: 100%;
  background: #ffffff;
  border: 2px solid #000000;
  border-radius: 8px;
  padding: 12px 20px 16px;
  margin-left: 15px;
  box-sizing: border-box;
}

#form-group-birthday select {
  background: #ffffff;
  border: 2px solid #000000;
  border-radius: 8px;
  padding: 12px 20px 16px;
  width: 30.9%;
}
.birthday-yyyy {
  margin-right: 10px;
}
.birthday-mm {
  margin-right: 10px;
  margin-left: 10px;
}
.birthday-dd {
  margin-left: 10px;
}
.label-title {
  display: block;
  padding: 8px 0;
  font-size: 20px;
  color: #000000;
  letter-spacing: 0;
}
#form-group-address select {
  background: #ffffff;
  border: 2px solid #000000;
  border-radius: 8px;
  padding: 12px 20px 16px;
  margin-bottom: 24px;
  width: 50%;
}
#form-group-address input {
  background: #ffffff;
  border: 2px solid #000000;
  border-radius: 8px;
  padding: 12px 20px 16px;
  display: block;
  width: 100%;
  box-sizing: border-box;
}
</style>
