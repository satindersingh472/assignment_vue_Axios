<template>
  <div>
    <button v-on:click="send_changed">S_n_a_k_e_J_o_k-e</button>
    <p>(click snake joke button to make a snake)</p>
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
  font-weight: bold;
  text-transform: uppercase;
}
</style>
