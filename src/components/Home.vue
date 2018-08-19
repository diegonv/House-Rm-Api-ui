<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button v-on:click="loadAll">Load</button>
    <h3>Elements: </h3>
    <div class='wrapper'>
      <template v-for="code in codes">
        <button :key="code.id" v-on:click="callCode(code.sendUrl)">{{code.displayName}}</button>
      </template>    
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Home',
  props: {
    msg: String
  },
  data () {
    return {
      codes: null,
    }
  },
  methods: {
    loadAll: function (event) {
      axios.get('mock.json')
           .then(response => {(this.codes = response.data);console.log(response)}
           )
           .catch(error => { console.log(error) });
    },
    callCode: function (url) {
      axios.get(url)
           .then(response => {console.log(response)}
           )
           .catch(error => { console.log(error) });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
}
</style>