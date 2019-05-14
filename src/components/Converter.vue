<template>
  <div class="converter">
    <h2>{{currA}} to {{currB}}</h2>
    <input type="text" v-model="currA_value" v-bind:placeholder="currA">
    <input type="button" value="Convert" v-on:click="converter">
    <h2>{{currB_value}}</h2>
  </div>
</template>

<script>
export default {
  name: "Converter",
  props: ["currA", "currB"],

  data() {
    return {
      currA_value: "",
      currB_value: 0
    };
  },  
  methods: {
    converter() {
      let from_to = this.currA + "_" + this.currB;
      let cA = this.currA;
      let cB = this.currB;

      let url =
        "https://free.currconv.com/api/v7/convert?q=" +
        from_to +
        "&compact=ultra&apiKey=ce3469123d58a045204c";

      //fetch url
      fetch(url)
        .then(res =>{
          return res.json();
        })
        .then(json => {          
          let cot = json[from_to];    
          console.log("Current value from 1 "+cA+" to 1 "+cB+" : " + cot);      
          this.currB_value = (cot * parseFloat(this.currA_value)).toFixed(2);
        })
        .catch(err => console.error(err));
    }
  }
};
</script>

<style scoped>
.converter{
  padding: 20px;
  max-width: 300px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}
</style>
