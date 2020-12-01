<template>
  <div >
    <div class="mx-auto">
    <h1>{{ msg }}</h1>
    <p> 
      {{ msg2 }}
      {{ message }}
  <input v-model="message">
    </p>
    <button type="button" class="btn btn-warning btn-sm" @click="editBook('hola')"> Botoncito </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function() {
    return {
      message: "gil", num2: ""
    }
  },   
  props: {
    msg: String,
    msg2: String,
    
  },
  methods: {
    getBooks: function() {
      const path = 'Hola has create con func';
      console.log(path);
        
    },
    addBook: function(payload) {
      const path = 'http://localhost:5001/books';
      console.log(path+payload);
    },
    editBook: function(cad) {
      console.log("edit "+cad+": "+this.message);

    },
  },

  created: function() {
    this.getBooks();
  }, 

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>