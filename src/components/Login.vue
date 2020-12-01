<template>
  <div class="mx-auto">
    
    <div class="bg-image mx-auto ">

          <div class="bg-text mx-auto">
        <h1 class="d-flex justify-content-center text-dark">LOGIN</h1>
        <hr />
        <br /><br />
        <alert :message="message" v-if="showMessage"></alert>
        
        <b-form @submit="onSubmit" @reset="onReset" class="w-100">
          <b-form-group
          class="text-dark text-left"
            id="form-title-group"
            label="Username:"
            label-for="form-title-input"
          >
            <b-form-input
              id="form-title-input"
              type="text"
              v-model="d.username"
              required
              placeholder="Username"
            >
            </b-form-input>
          </b-form-group>
          <b-form-group
          class="text-dark text-left"
            id="form-author-group"
            label="Password:"
            label-for="form-author-input"
          >
            <b-form-input
              id="form-author-input"
              type="password"
              v-model="d.password"
              required
              placeholder="PASSWORD"
              >s
            </b-form-input>
          </b-form-group>

          <b-button-group>
            <button type="button" class="btn btn-success btn-sm" v-on:click="back()">Cancel</button>
            <b-button type="submit" variant="primary">Submit</b-button>
            <b-button type="reset" variant="danger">Reset</b-button>
          </b-button-group>
        </b-form>
      </div>
      </div>
  </div>
</template>

<script>
import Alert from "./Alert.vue";
import client from "../api";

export default {
  name: "LoginForm",
  data: function () {
    return {
      message: "",
      showMessage: false,
      d: {
        Email: "",
        Password: "",
      },
    };
  },
  components: {
    alert: Alert,
  },
  methods: {
    makeToast: function (titulo, texto, tipo) {
      this.toastCount++;
      this.$bvToast.toast(texto, {
        title: titulo,
        variant: tipo,
        autoHideDelay: 5000,
        appendToast: true,
      });
    },
    /*back: function () {
      this.$router.push("/persons");
    },*/

    login: function (payload) {
      client
        .post("/usuariologin/login", payload)
        .then((res) => {
          console.log(payload);

          // console.log('set');
          let credentials = {
            "token":res.data.token,
            "user":res.data,
          };
          //console.log(credentials.token);
          localStorage.setItem("user", JSON.stringify(credentials));

          //console.log('get');
          //let user = JSON.parse(localStorage.getItem("user"));
          //if (user != null) {
          //  console.log(user.token);
          //}

          this.message = "Login correcto";
          this.showMessage = true;
          this.makeToast("Hecho", "Login ok", "success");
          //this.$router.push("/persons");
        })
        .catch((error) => {
          console.log(error);
        });
    },
    initForm: function () {
      //this.d.ID = '';
      this.d.Email = "";
      this.d.Password = "";
    },
    onSubmit: function (evt) {
      evt.preventDefault();

      const payload = {
        email: this.d.Email,
        password: this.d.Password,
      };

      this.login(payload);

      this.initForm();
    },
    onReset: function (evt) {
      evt.preventDefault();
      //this.initForm();
      evt.target.reset();
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
body, html {
  height: 100%;
}

* {
  box-sizing: border-box;
}

.bg-image {
 /*background-image: url("/assets/bg-blur.png");*/
  background-color: #7fb8fa;
  width: 60%;
}

/* Position text in the middle of the page/image */
.bg-text {
  color: white;
  font-weight: bold;
  border: 3px solid #1b26bd;
  width: 100%;
  padding: 20px;
  text-align: center;
}
</style>