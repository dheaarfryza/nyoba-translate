<template>
      <div>
      <label>Input text</label><br />
      <textarea v-model="inputText"></textarea><br />
    <label>Choose language</label><br />
    <select v-model="inputLanguage">
      <option v-for="language in languageList" :value="language.code" :key="language.code">
        {{ language.name }}
      </option>
    </select><br />
    <select v-model="outputLanguage">
      <option v-for="language in languageList" :value="language.code" :key="language.code">
        {{ language.name }}
      </option>
    </select><br />
    <label>Output text</label><br />
      <textarea v-model="outputText"></textarea><br />
    <button v-if="input.text != null && input.name != null" @click="translateText">Play</button>
    <!-- <p v-show="isPlay">Playing ...</p>  -->
  </div>
</template>

<script>
import axios from 'axios';
import languageList from './data/languages.js';

export default {
  data: {
    inputText:"",
    outputText:"",
    languageList,
    inputLanguage: "id",
    outputLanguage: "en"
  },
  methods: {
    translateText() {
      const encodedParams = new URLSearchParams();
      encodedParams.append("q", inputText);
      encodedParams.append("target", inputLanguage);
      encodedParams.append("source", outputLanguage);

const options = {
  method: 'POST',
  url: 'https://google-translate1.p.rapidapi.com/language/translate/v2',
  headers: {
    'content-type': 'application/x-www-form-urlencoded',
    'Accept-Encoding': 'application/gzip',
    'X-RapidAPI-Key': '97d71aea4emshe9cd36f1015a5c4p17cfe0jsn039ff4af3c8f',
    'X-RapidAPI-Host': 'google-translate1.p.rapidapi.com'
  },
  data: encodedParams
};
axios.request(options).then(function (response) {
	console.log(response.data);
}).catch(function (error) {
	console.error(error);
});
    }
  },
  mounted() {
    this.translateText();
  }
}
</script>