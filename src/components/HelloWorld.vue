<template>
  <div class="col-md-6 offset-md-3">

    <table class="table table-inverse col-md-6 offset-md-3">
    <thead>
      <tr>
        <th>Location Address</th>
        <th>Location Name</th>
        <th>Lat/Long</th>
        <th>Remove</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(data, index) in arr" v-if="arr.removed == 'false'">
        <td>{{data.location_address}}</td>
        <td>{{data.location_name}}</td>
        <td>{{data.lat}} "," {{data.long}}</td>
        <td><button v-on:click="removeSkimmer(data.uuid, index)">Remove</button></td>
      </tr>
    </tbody>
</table>



</div>
</template>

<script>
import Vue from 'vue'
import Axios from 'axios'

export default {
  name: 'HelloWorld',
  data(){
    return{
      responseData: [],
      arr: []
    }
  },
  methods: {
    getAll: function() {
      let that = this;
      Axios.get('https://overlook-api.herokuapp.com/get-all-skimmers').then(function(res) {
        that.responseData = res.data;
        console.log('Response', JSON.stringify(res.data));
        Object.keys(that.responseData).forEach(function (key) {
            var val = that.responseData[key];
            that.arr.push(val);
            // use val
        });
      }).catch(function(err) {
        console.log("There is an error here");
        console.log(err);
      })
    },
    removeSkimmer: function(UUID, index) {
      let that = this;
      Axios.post('https://overlook-api.herokuapp.com/skimmer-removed', {uuid: UUID}).then(function(res) {
        console.log("This is the response for remove function: ", res);
        if(res.data.removed) {
          that.arr.splice(index, 1);
        }
      }).catch(function(err) {
        console.log("This is an error");
        console.log(err);
      });
    }
  },
  created: function() {
    this.getAll();
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
