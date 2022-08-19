<template>
  <div>
    <button @click="send_changed">Normal Joke</button>
    <p>(click normal joke button to change the joke back to normal)</p>
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
    // send changed will send the joke from data as is because it should make the string normal back again
    // it will emit the global event changed joke along with joke from data unchanged 
    // so that the listener component will get initial unchanged string and use that string to make changes on the page
    send_changed() {
      this.$root.$emit(`changed_joke`, this.joke);
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
