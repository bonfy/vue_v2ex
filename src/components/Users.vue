<template>
  <div class="hello">
    <ul>
        <li v-for="user in users">
            {{user.name}}:{{user.email}}
        </li>
    </ul>

    <input type="text" v-model="zipcode" />
    <span>{{zipcode}}</span>

  </div>
</template>

<script>
import _ from 'lodash';

export default {
  name: 'hello',
  data () {
    return {
      users: [],
      zipcode: ''
    }
  },
  methods: {
    recodeZip: _.debounce(function () {
      console.log(this.zipcode)
    }, 500)
  },
  watch: {
    zipcode: function(val) {
      if (val.length == 5) {
        console.log('find val ...');
        this.recodeZip()
      }
    }
  },
  created: function (){
    this.$http.get('https://jsonplaceholder.typicode.com/users')
      .then(function(response) {
        console.log(response.data);
        this.users = response.data;
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
