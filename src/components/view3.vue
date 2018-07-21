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
        <input type="text" placeholder="1234567890123456"/>
      </div>
      <div class="form-group">
        <label>Cardholder Name</label>
        <input type="text" placeholder="Elon Musk"/>
      </div>
      <div class="form-group">
        <label>Bank Name</label>
        <input type="text" placeholder="City Group"/>
      </div>
      <div class="form-group">
        <label>CVV</label>
        <input type="number" placeholder="123"/>
      </div>
      <div class="form-group">
        <label>Expire Date</label>
        <select>
            <option v-for="(MM,index) in 12" :key="index">{{MM}}</option>
        </select> <select>
            <option v-for="(DD,index) in 31" :key="index">{{DD}}</option>
        </select>
      </div>
      <input type="button" value="DONE">
    </form>
  </div>
</template>

<script>
export default {
  name: "view3",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
