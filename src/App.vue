<template>
  <div id="app">
    <!-- joke button to display and make an api call -->
    <joke-button></joke-button>
    <!-- paragraph div to display joke on string and if no joke is present then msg is displayed for instructions -->
    <div class="paragraph">
      <div v-if="joke !== undefined">
      <p>{{joke}}</p>
      </div>
    <div v-else-if ="joke === undefined">
      <p>click the button to see random joke<br>and below buttons are to modify the text<br>always click joke button to get a new joke</p>
    </div>
    </div>
    <!-- normal joke component will set the joke to normal -->
    <normal-joke></normal-joke>
    <!-- snake joke will put underscore after every word -->
    <snake-joke></snake-joke>
    <!-- loud joke component will make all the letters in a string uppercase -->
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
    // joke recieved method will display a joke when api is called by pressing joke button
    joke_recieved(random_joke) {
      this.joke = random_joke;
    },
    // show changed method will get called by global event happening when event lifecycle is on mounted
    // it will store any changes to joke and that joke will get displayed in the html
    show_changed(random_joke){
      if(this.joke !== undefined){
        this.joke = random_joke;
      }
    },
  },
  mounted () {
    // joke sent is a global event coming from jokebutton
    this.$root.$on(`joke_sent`,this.joke_recieved);
    // changed joke global event is bringing the change emited by other components and calling then show changed method
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
