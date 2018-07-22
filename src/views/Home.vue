<template>
  <div class="home">
   <a href="#" @click="changeView(0)">view0</a>/
   <a href="#" @click="changeView(1)">view1</a>/
   <a href="#" @click="changeView(2)">view2</a>/
   <a href="#" @click="changeView(3)">view3</a>/
   <a href="#" @click="changeView(4)">view4</a>
   <view0 v-if="currentView===0" @goNext="changeView(1)"/>
   <view1 v-else-if="currentView===1" @goNext="changeView(2)"/>
   <view2 v-else-if="currentView===2"/>
   <view3 v-else-if="currentView===3"/>
   <view4 v-else-if="currentView===4"/>
  </div>
</template>

<script>
// @ is an alias to /src
import view0 from "@/components/view0.vue";
import view1 from "@/components/view1.vue";
import view2 from "@/components/view2.vue";
import view3 from "@/components/view3.vue";
import view4 from "@/components/view4.vue";

export default {
  name: "home",
  components: {
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
pre {
  font-size: 2rem;
  background-color: cadetblue;
}
</style>

