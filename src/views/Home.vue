<template>
  <div class="home">
   <statebar :states="states"></statebar>
   <view0 v-if="currentView===0" @goNext="changeView(1)"/>
   <view1 v-else-if="currentView===1" @goNext="changeView(2)"/>
   <view2 v-else-if="currentView===2" @goNext="changeView(3)"/>
   <view3 v-else-if="currentView===3" @goNext="changeView(4)"/>
   <view4 v-else-if="currentView===4" @goNext="changeView(0)"/>
  </div>
</template>

<script>
// @ is an alias to /src
import statebar from "@/components/stateBar.vue";
import view0 from "@/components/view0.vue";
import view1 from "@/components/view1.vue";
import view2 from "@/components/view2.vue";
import view3 from "@/components/view3.vue";
import view4 from "@/components/view4.vue";

export default {
  name: "home",
  components: {
    statebar,
    view0,
    view1,
    view2,
    view3,
    view4
  },
  data: function() {
    return {
      currentView: 0
    };
  },
  computed: {
    states: function() {
      let ret = [];
      let v = this.currentView;
      for (let i = 0; i < 5; i++) {
        if (i < v) {
          ret.push(1);
        } else if (i > v) {
          ret.push(-1);
        } else {
          ret.push(0);
        }
      }

      return ret;
    }
  },

  methods: {
    changeView: function(i) {
      this.currentView = i;
    }
  }
};
</script>
<style>
* {
  text-decoration: none;
}
.form-area {
  text-align: start;
  width: 40%;
  margin: auto;
}
@media only screen and (max-width: 1200px) {
  .form-area {
    width: 60%;
  }
}
@media only screen and (max-width: 600px) {
  .form-area {
    width: 95%;
  }
}
.button {
  text-align: center;
  background: #0275d8;
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
.button[disabled] {
  background: #bee1ff;
}
select {
  -webkit-appearance: none;
  font-size: 20px;
  box-sizing: border-box;
  padding: 12px 20px;
}
input[type="email"],
input[type="text"],
input[type="password"] {
  font-size: 20px;
  box-sizing: border-box;
  padding: 12px 20px;
}
</style>

