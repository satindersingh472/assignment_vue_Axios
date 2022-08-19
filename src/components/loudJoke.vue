<template>
  <div>
    <button @click="send_changed">LOUD JOKE</button>
    <p>(click the LOUD JOKE button to see all the letters UPPERCASE)</p>
  </div>
</template>

<script>
export default {
  mounted() {
   this.$root.$on(`joke_sent`, this.convert_joke);
  },
  methods: {
    convert_joke(random_joke) {
      this.joke = random_joke;
    },
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
    font-weight: bold;
}
</style>