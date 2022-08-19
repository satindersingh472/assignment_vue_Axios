<template>
  <div>
    <button @click="send_changed">LOUD JOKE</button>
    <p>(click the LOUD JOKE button to see all the letters UPPERCASE)</p>
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
    // send changed will emit the gobal event changed joke after changing the string to uppercase
    send_changed() {
      this.$root.$emit(`changed_joke`, this.joke.toLocaleUpperCase(`en-US`));
    },
  },
  data() {
    return {
      joke: undefined,
    };
  }
};
</script>

<style scoped>
button{
    padding: 5px;
    font-size: 1.5rem;
}
</style>