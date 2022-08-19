<template>
  <div>
    <!-- button will fire the send changed method -->
    <button v-on:click="send_changed">S_n_a_k_e_J_o_k-e</button>
    <p>(click snake joke button to make a snake)</p>
  </div>
</template>

<script>
export default {
  mounted() {
    // following line will listen for global event  joke sent
    // and after listening to the event it will fire the convert joke method
    this.$root.$on(`joke_sent`, this.convert_joke);
  },
  methods: {
    // convert joke method will store whatever value is recieving from global event
    // to the joke inside data
    convert_joke(random_joke) {
      this.joke = random_joke;
    },
    // send changed will emit the global event changed joke after making chnages to the joke
    // it will convert whitespace in a string into underscores and send them with changed joke global event
    send_changed() {
      this.$root.$emit(`changed_joke`, this.joke.replaceAll(" ","_"));
    },
  },
  data() {
    return {
      joke: undefined
    };
  },
};
</script>

<style scoped>
p{
  color: black;
}
button{
  padding: 5px;
  text-transform: uppercase;
  font-size: 1.5rem;
}
</style>
