<template>
  <div class="container bg-white tableall">
    <div class="container h-10">
      <div class="row h-100 align-items-center justify-content-center text-center">
        <div class="col-lg-10 align-self-end">
           <div>
        <h1>CRUD Persons</h1>
        <hr class="divider my-2" />
        <br /><br />
        <alert :message="message" v-if="showMessage"></alert>

        <br /><br />
        <table class="table table-hover table-striped">
          <thead class="thead-warning">
            <tr>
              <th scope="col">#</th>
              <th scope="col">Name</th>
              <th scope="col">Age</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(d, index) in list" :key="index">
              <td>{{ d.ID }}</td>
              <td>{{ d.name }}</td>
              <td>{{ d.age }}</td>

              <td>
                <div class="btn-group" role="group">
                  <button type="button" class="btn btn-warning btn-sm" @click="edit(d.ID)"><i class="fas fa-pen"></i> Update </button>
                  <button type="button" class="btn btn-danger btn-sm ml-2" @click="onDelete(d)"><i class="fas fa-trash-alt"></i> Delete</button>
                </div>               
              </td>
            </tr>
          </tbody>
        </table>
                <button type="button" class="btn btn-success btn-sm mb-2" v-on:click="add()">
          Add Person
        </button>
      </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Alert from "./Alert.vue";
import client from "../api";

export default {
  name: "Person",
  data: function () {
    return {
      list: [],
      message: "",
      showMessage: false,
    };
  },
  components: {
    alert: Alert,
  },
  methods: {
    edit: function (id) {
      this.$router.push("/persons/form/" + id);
    },
    add: function () {
      this.$router.push("/persons/form");
    },
    getList: function () {
      client
        .get("/v1/persons")
        .then((res) => {
          this.list = res.data.r;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    onDelete: function (d) {
      var r = confirm("Eliminar ?");
      if (r == true) {
        this.delete(d.ID);
      }
    },
    delete: function (id) {
      client
        .delete(`/v1/persons/${id}`)
        .then(() => {
          this.getList();
          this.message = "Person removed!";
          this.showMessage = true;
        })
        .catch((error) => {
          console.error(error);
          this.getList();
        });
    },
  },

  created: function () {

    this.message = this.$route.query.msg;
    //console.log(this.message);

    if (typeof(this.message) !=='undefined') {// || this.message !== null
      this.showMessage = true;
     // this.makeToast("Hecho", this.message, "success");
    }

    this.getList();
  },
};
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
.hello {
  color: #42b983;
}
</style>