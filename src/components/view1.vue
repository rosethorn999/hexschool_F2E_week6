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
        <input type="text" placeholder="example@eamil.com"/>
      </div>
      <div class="form-group">
        <label>Phone*</label>
        <input type="telphone" placeholder="0912345678"/>
      </div>
      <div class="form-group">
        <label>Birth Date(optional)</label>
        <select>
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
        <select>
            <option v-for="(DD,index) in 31" :key="index">{{DD}}</option>
        </select>
        <select>
            <option v-for="(DD,index) in 31" :key="index">{{DD}}</option>
        </select>
        <input type="text"/>
      </div>
      <input type="button" value="SUBMIT & NEXT">
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
    return {};
  },
  computed: {
    YYYYs: function() {
      let ret = [];
      for (let i = 1950; i < 2000; i++) {
        ret.push(i);
      }
      return ret;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
