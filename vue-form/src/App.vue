<template>
  <form v-on:submit.prevent="submitForm">
    <div>
      <label for="username">id: </label>
      <input id="username" type="text" v-model="useranme">
    </div>
    <div>
        <label for="password">pw: </label>
        <input id="password" type="password" v-model="password">
    </div>
    <button type="submit">login</button>
  </form>
</template>

<script>
import axios from 'axios';

export default {
    data: function() {
        return {
            useranme: '',
            password: '',
        }
    },
    methods: {
        submitForm: function() {
            // event.preventDefault();
            console.log(this.useranme,this.password);
            var url = 'https://jsonplaceholder.typicode.com/users';
            var data = {
                username: this.useranme,
                password: this.password
            }
            axios.post(url,data)
            .then(function(response){
                console.log(response);
            })
            .catch(function(error){
                console.log(error);
            })
        }
    }
};
</script>

<style></style>
