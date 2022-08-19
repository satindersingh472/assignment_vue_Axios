<template>
  <div id="app">
    <joke-button></joke-button>
    <div class="paragraph">
      <div v-if="joke !== undefined">
      <p>{{joke}}</p>
      </div>
    <div v-else-if ="joke === undefined">
      <p>click the button to see random joke<br>and below buttons are to modify the text<br>always click joke button to get a new joke</p>
    </div>
    </div>
    <normal-joke></normal-joke>
    <snake-joke></snake-joke>
    <loud-joke></loud-joke>
  </div>
</template>

<script>
import JokeButton from '@/components/jokeButton.vue';
import SnakeJoke from "@/components/snakeJoke.vue";
import NormalJoke from '@/components/normalJoke.vue';
import LoudJoke from '@/components/loudJoke.vue';
export default {
  name: 'App',
  components: {
    JokeButton,
    SnakeJoke,
    NormalJoke,
    LoudJoke
  },
  methods: {
    joke_recieved(random_joke) {
      this.joke = random_joke;
    },
    show_changed(random_joke){
      if(this.joke !== undefined){
        this.joke = random_joke;
      }
    },
  },
  mounted () {
    this.$root.$on(`joke_sent`,this.joke_recieved);
    this.$root.$on(`changed_joke`,this.show_changed);
  },
  data() {
    return {
      joke: undefined,
    }
  },
}
</script>

<style scoped> 
#app{
  text-align: center;
  display: grid;
  gap: 20px;
}
p{
  color:royalblue
}
</style>
