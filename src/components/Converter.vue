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
      let cA = this.currA;
      let cB = this.currB;
      let amount = parseFloat(this.currA_value);

      if (isNaN(amount)) {
        this.currB_value = 0;
        return;
      }

      // Frankfurter (ECB rates, no API key). The old currconv free API is shut down.
      let url =
        "https://api.frankfurter.dev/v1/latest?base=" + cA + "&symbols=" + cB;

      fetch(url)
        .then(res => {
          if (!res.ok) throw new Error("HTTP " + res.status);
          return res.json();
        })
        .then(json => {
          let cot = json.rates[cB];
          // eslint-disable-next-line no-console
          console.log("Current value from 1 " + cA + " to 1 " + cB + " : " + cot);
          this.currB_value = (cot * amount).toFixed(2);
        })
        // eslint-disable-next-line no-console
        .catch(err => console.error(err));
    }
  }
};
</script>

<style scoped>
.converter{
  padding: 20px;
  max-width: 300px;
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  box-shadow: 0 4px 8px 0 var(--shadow);
  color: var(--text);
}
.converter input {
  background: var(--input-bg);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 6px 10px;
  margin: 4px;
}
.converter input[type="button"] {
  background: var(--accent);
  color: #fff;
  border: none;
  cursor: pointer;
}
.converter input[type="button"]:hover {
  background: var(--accent-hover);
}
</style>
