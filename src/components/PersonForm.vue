<template>
  <div class="container bg-white tableall">
    <div class="container h-10">
      <div class="row h-100 align-items-center justify-content-center text-center">
        <div class="col-lg-10 align-self-end">
                  <div>
        <h1>Person Form</h1>
        <hr />
        <br />
        <alert :message="message" v-if="showMessage"></alert>
        <button
          type="button"
          class="btn btn-success btn-sm"
          v-on:click="back()"
        >
          Regresar
        </button>
        <p class="text-left">ID= {{ d.ID }}</p>

        <b-form @submit="onSubmit" @reset="onReset" class="w-100">
          <b-form-group
           class="text-left"
            id="form-title-group"
            label="Title:"
            label-for="form-title-input"
          >
            <b-form-input
              id="form-title-input"
              type="text"
              v-model="d.name"
              required
              placeholder="Enter title"
            >
            </b-form-input>
          </b-form-group>
          <b-form-group
           class="text-left"
            id="form-author-group"
            label="Author:"
            label-for="form-author-input"
          >
            <b-form-input
              id="form-author-input"
              type="text"
              v-model="d.age"
              required
              placeholder="Enter author"
            >
            </b-form-input>
          </b-form-group>

          <b-button-group class="mb-2">
            <b-button type="submit" variant="primary"><i class="fas fa-check"></i> Submit</b-button>
            <b-button  class="ml-2" type="reset" variant="danger"><i class="fas fa-sync"></i>  Reset</b-button>
          </b-button-group>
        </b-form>
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
  name: "PersonForm",
  data: function () {
    return {
      message: "",
      showMessage: false,
      d: {
        ID: "",
        name: "",
        age: "",
      },

    };
  },
  components: {
    alert: Alert,
  },
  methods: {
    
    back: function () {
      this.$router.push("/persons");
    },

    create: function (payload) {
      client
        .post("/v1/persons", payload)
        .then(() => {
          console.log(payload);

          this.message = "Person added!";
          this.showMessage = true;
          this.$router.push("/persons?msg="+this.message);
        })
        .catch((error) => {
          this.message = error;
          this.showMessage = true;
          console.log(error);
        });
    },
    initForm: function () {
      //this.d.ID = '';
      this.d.name = "";
      this.d.age = "";
    },
    onSubmit: function (evt) {
      evt.preventDefault();

      const payload = {
        name: this.d.name,
        age: this.d.age,
      };
      if (this.d.ID > 0) {
        this.update(payload, this.d.ID);
      } else {
        this.create(payload);
      }
      this.initForm();
    },
    onReset: function (evt) {
      evt.preventDefault();
      //this.initForm();
      evt.target.reset();
    },

    getById: function (id) {
      client
        .get(`/v1/persons/${id}`)
        .then((res) => {
          this.d = res.data;
        })
        .catch((error) => {
          this.message = error;
          this.showMessage = true;
          console.error(error);
        });
    },

    update: function (payload, id) {
      client
        .put(`/v1/persons/${id}`, payload)
        .then(() => {
          console.log(payload);

          this.message = "Person updated!";
          this.showMessage = true;
          this.$router.push("/persons?msg="+this.message);
        })
        .catch((error) => {
          this.message = error;
          this.showMessage = true;
          console.error(error);
          //this.getBooks();
        });
    },
  },

  created: function () {
    this.d.ID = this.$route.params.id;
    if (this.d.ID > 0) {
      this.getById(this.d.ID);
    }
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