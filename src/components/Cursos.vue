<template>
  <div class="container bg-white tableall">
     <div class="container h-10">
        <div class="row h-100 align-items-center justify-content-center text-center">
          <div class="col-lg-10 align-self-end">
            <div >
              <h1>CRUD Cursos</h1>
              <hr class="divider my-4" />
              <alert :message="message" v-if="showMessage"></alert>
              
              <br /><br />
              <table class="table table-hover table-striped">
                <thead class="thead-dark">
                  <tr>
                    <th scope="col">ID</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">Detalle</th>
                    <th scope="col">Sesiones</th>
                    <th scope="col">Horas</th>
                    <th></th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(d, index) in list" :key="index">
                    <td>{{ d.ID }}</td>
                    <td>{{ d.idTipoUnidad }}</td>
                    <td>{{ d.nombre }}</td>
                    <td>{{ d.sesiones }}</td>
                    <td>{{ d.horas }}</td>
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
                Agregar Curso
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
  name: "Cursos",
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
      this.$router.push("/cursos/form/" + id);
    },
    add: function () {
      this.$router.push("/cursos/form");
    },
    getList: function () {
      client
        .get("/v1/unidadAcademica/2")
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
        .delete(`/v1/unidadAcademica/2${id}`)
        .then(() => {
          this.getList();
          this.message = "Curso eliminado!";
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
<style >
.tableall{
  -webkit-border-radius: 15px;
  -moz-border-radius: 15px;
  border-radius: 15px;
}
</style>