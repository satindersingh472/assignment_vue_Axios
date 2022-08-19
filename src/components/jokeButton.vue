<template>
  <div>
    <button v-on:click="send_joke">Joke Button</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {},
  methods: {
    send_joke() {
           axios.request({
          url: `https://ron-swanson-quotes.herokuapp.com/v2/quotes`,
        })
        .then((response) => {
          this.joke = response[`data`][0];
            this.$root.$emit(`joke_sent` , this.joke);
        })
        .catch((error) => {
          this.joke = error;
        });

      
    }
  },
  data() {
    return {
      joke: []
    };
  },
};
</script>

<style scoped>
button {
  padding: 10px;
  font-size: 1.5rem;
}
</style>
