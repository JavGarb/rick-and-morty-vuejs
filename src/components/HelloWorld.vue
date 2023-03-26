<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
import { tSLiteralType } from '@babel/types';

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Fasthand&display=swap");

.hello {
  color: blue;
  font-family: "Fasthand", cursive;
  font-size: xxx-large;
  text-shadow: 4px 0px 20px magenta;
}



</style>
