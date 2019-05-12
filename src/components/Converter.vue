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
//sVR3vtn6CnXEVPB6DSXS7vebcXavtk  = API KEY
//EXAMPLE URL : https://www.amdoren.com/api/currency.php?api_key=IBZzdLmM2yCYaXjgTZ6x&from=EUR&to=GBP&amount=50
  methods: {
    converter() {       
        let url = "https://www.amdoren.com/api/currency.php?api_key=sVR3vtn6CnXEVPB6DSXS7vebcXavtk&from="+this.currA+"&to="+this.currB+"&amount="
        +this.currA_value;

        //fetch url
        
        
    }
  }
};
</script>


<style scoped>
</style>
