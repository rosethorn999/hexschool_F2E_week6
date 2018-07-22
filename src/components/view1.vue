<template>
  <div class="view1">
    <pre>::view1::</pre>
    <h1>General Infomation</h1>
    <p>
      Tell us who you are!
    </p>
    <form>
      <div class="form-group">
        <label>Name(optional)</label>
        <input type="text" placeholder="example@eamil.com" v-model="name"/>
      </div>
      <div class="form-group">
        <label>Phone</label>
        <input type="telphone" placeholder="0912345678" v-model="telphone"/>
        <div class="alarm" v-show="telphoneError">NUMBER ONLY</div>
      </div>
      <div class="form-group">
        <label>Birth Date(optional)</label>
        <select v-model="YYYY">
            <option v-for="(YYYY,index) in YYYYs" :key="index">{{YYYY}}</option>
        </select>
        <select>
            <option v-for="(MM,index) in 12" :key="index">{{MM}}</option>
        </select>
        <select>
            <option v-for="(DD,index) in 31" :key="index">{{DD}}</option>
        </select>
      </div>
       <div class="form-group">
        <label>Address</label>
        <select v-model="city">
            <option v-for="(city,index) in citys" :key="index" :value="index">{{city}}</option>
        </select>
        <select v-model="dist">
            <option v-for="(dist,index) in districts" :key="index" :value="index">{{dist}}</option>
        </select>
        <input type="text" v-model="address" placeholder="detail address"/>
         <div class="alarm" v-show="addressError">REQUIRED FILED</div>
      </div>
      <input type="button" value="SUBMIT & NEXT" :disabled="formError" @click="send">
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
</style>
