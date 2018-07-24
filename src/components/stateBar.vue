<template>
  <div class="stateBar">
    <div v-for="(item,index) in states" :key="index">
      <div class="bar" :class="getState(item)" v-if="index!==0">
        <i class="fas fa-minus"></i>
        <i class="fas fa-minus"></i>
      </div>
      <div class="dot" :class="getState(item)">
        <div v-html="getIcon(item)"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "state-bar",
  props: {
    states: {
      type: Array, // Object or array defaults must be returned from a factory function
      default: function() {
        return [1, 1, 0, -1, -1];
      }
    }
  },
  data: function() {
    return {};
  },
  mounted: function() {},
  methods: {
    getState: function(item) {
      let ret = "";
      switch (item) {
        case -1: //未觸發
          ret = "notyet";
          break;
        case 0: //正被執行
          ret = "active";
          break;
        case 1: //已完成
          ret = "done";
          break;
      }
      return ret;
    },
    getIcon: function(item) {
      let ret = "";
      switch (item) {
        case -1: //未觸發
          ret = '<i class="far fa-circle"></i>';
          break;
        case 0: //正被執行
          ret = '<i class="far fa-dot-circle"></i>';
          break;
        case 1: //已完成
          ret = '<i class="far fa-check-circle"></i>';
          break;
      }
      return ret;
    }
  },
  watch: {},
  computed: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.stateBar {
  color: #c0e2ff;
  margin: 50px auto;
  text-align: center;
}
.stateBar > div {
  display: inline-block;
}
.bar {
  width: 2rem;
  height: 5px;
  display: inline-block;
}
.dot {
  background: transparent;
  width: 1rem;
  display: inline-block;
}

.notyet {
  /* background: #c0e2ff; */
}
.active {
  color: #0275d8;
}
.done {
  color: #0275d8;
}
</style>
