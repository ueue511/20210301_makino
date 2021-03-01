<template>
  <div id="app">
      <input type="tel" v-model="postalCodeNum" placeholder="ハイフンなしの7桁入力" required maxlength=7 oninput="value = value.replace(/[^0-9]+/i,'');" />
      <input type="submit" value="住所自動入力" @click="PostCode_Searce"/>
      <p>Address: {{ postaCode }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      postaCode: "",
      postalCodeNum: ""
    }
  },
  methods: {
    async PostCode_Searce() {
      const item = await axios.get(`https://apis.postcode-jp.com/api/v3/postcodes?postcode=${this.postalCodeNum}&general=true`);
      const postaCodeData = item.data;
      this.postaCode = postaCodeData.data[0].allAddress;
    }
  }
};
</script>


