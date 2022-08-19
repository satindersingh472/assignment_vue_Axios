<template>
  <div>
    <!-- send joke button will call api for random jokes -->
    <button v-on:click="send_joke">Joke Button</button>
  </div>
</template>

<script>
// importing axios library from axios 
import axios from "axios";
export default {
  components: {},
  methods: {
    // send joke method will call api when send joke button is clicked
    // after successfully getting response it will store the data (string) into jokes inside data
    // then it will emit the global event joke sent and sending the joke from data with it
    send_joke() {
           axios.request({
          url: `https://ron-swanson-quotes.herokuapp.com/v2/quotes`,
        })
        .then((response) => {
          // following line will store the string from response[`data`][0] to this.joke
          this.joke = response[`data`][0];
          // following line will help emit joke sent globally
            this.$root.$emit(`joke_sent` , this.joke);
        })
        .catch((error) => {
          this.joke = error;
        });

      
    }
  },
  data() {
    return {
      joke: undefined
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
