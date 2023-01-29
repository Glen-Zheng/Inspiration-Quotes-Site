<script setup>
import { ref } from "vue";
import axios from "axios";

let quoteNumber = Math.floor(Math.random() * 1643);
let quotes = ref();

quotes.value = await axios.get("https://type.fit/api/quotes");
</script>

<template>
  <h2 id="title">Quote Of The Day</h2>
  <h1 class="daily">{{ quotes.data[quoteNumber].text }}</h1>
  <p class="daily">{{ quotes.data[quoteNumber].author }}</p>
  <p class="daily" v-if="!quotes.data[quoteNumber].author">Anonymous</p>

  <br />
  <br />
  <div id="flex">
    <div v-for="quote in quotes.data" id="quotes-view">
      <p id="quotes-style">{{ quote.text }}</p>
      <p id="quotes-author">- {{ quote.author }}</p>
    </div>
  </div>
</template>

<style scoped>
#quotes-view {
  border: 2px solid black;
  background: coral;
  width: 15%;
  aspect-ratio: 10/11;
  margin: 20px auto 20px auto;
  box-shadow: 3px 3px rgb(5, 55, 86);
}

#flex {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin: 0 20px 10px 20px;
}

.daily {
  text-align: center;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  font-size: 3rem;
  margin-left: 5%;
  margin-right: 5%;
  color: darkslateblue;
}

#quotes-style {
  font-size: 2rem;
  font-family: Georgia, "Times New Roman", Times, serif;
  text-align: center;
}

#quotes-author {
  font-size: 1rem;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  text-align: center;
}

#title {
  text-align: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  text-decoration: underline;
  font-size: 4.5rem;
  color: rgb(5, 64, 4);
}
</style>
