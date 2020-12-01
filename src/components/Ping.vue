<template>
  <div>
     <div class="container h-10">
        <div class="row h-100 align-items-center justify-content-center text-center">
          <div class="col-lg-10 align-self-end">
            <button type="button" class="btn btn-primary">{{ msg }}</button>
          </div>
        </div>
      </div>
  </div>
</template>
<script>
//import axios from 'axios';
import client from "../api";

export default {
  name: 'Ping',
  data: function() {
    return {
      msg: "ping"
    }
  },   
  methods: {
    getMessage: function() {
      //const path = 'http://localhost:8081/v1/ping';
      client.get('/v1/ping')
        .then((res) => {
          this.msg = res.data;
        })
        .catch((error) => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
  },
  created: function() {
    this.getMessage();
  }, 
}
</script>