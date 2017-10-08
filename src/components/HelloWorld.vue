<template>
  <div><span>Hello World!</span></div>
</template>

<script>
import Axios from 'axios'

export default {
  name: 'HelloWorld',
  methods: {
    someMethod() {
      console.log('ayyy lmao')
      Axios.get('https://overlook-api.herokuapp.com/get-all-skimmers', {
        headers: {
        'Access-Control-Allow-Origin': '*'
      }
      }).then(function(res) {
        console.log('Response', res);
      }).catch(function(err) {
        console.log(err);
      })
    }
  },
  created: function() {
    this.someMethod();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
</style>
