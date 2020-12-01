<template>
  <div id="applms">
    <nav class="navbar navbar-expand-lg fixed-top navbar-light py-3">
      <router-link to="/" class="navbar-brand text-light">Home</router-link>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item ">
            <router-link to="/ping" class="nav-link text-light">Ping</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/persons" class="nav-link text-light">Person</router-link>
          </li>    
          <li class="nav-item">
            <router-link to="/cursos" class="nav-link text-light">Curso</router-link>
          </li>   
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <router-link to="/logout" class="nav-link text-danger"><i class="fas fa-external-link-alt"></i>  Logout</router-link>
          <router-link to="/login" class="nav-link text-warning"><i class="fas fa-sign-in-alt"></i>  Login</router-link>
        </form>
      </div>
    </nav>

    <div class="masthead">
            <div class="container h-10">
              <div class="row h-100 align-items-center justify-content-center text-center">
                <div class="col-lg-10 align-self-end">
                    <h1 class="text-uppercase text-white font-weight-bold">VUE + GO CRUD API</h1>
                    
                    </div>
                    <div class="col-lg-8 align-self-baseline">
                    <p class="text-white-75 font-weight-normal text-light mb-5"> ( ͡° ͜ʖ ͡°)</p>
                </div>
              </div>
            </div>
     <!--   <b-nav>
          <b-nav-item active to="/">Home</b-nav-item>
          <b-nav-item to="/ping">Ping</b-nav-item>
          <b-nav-item to="/persons">CRUD Person</b-nav-item>
          <b-nav-item to="/login">Login</b-nav-item>
          <b-nav-item to="/logout">Salir</b-nav-item>
          <b-nav-item to="/cursos">Cursos</b-nav-item>
        </b-nav> -->
        <b-container>
          <router-view/>
        </b-container >
    </div>

  
  </div>
</template>


<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;700&display=swap');

.applms{
  font-family: 'Montserrat', sans-serif;
}
.iconinfo{
  color:#5222A1;
}
.iconsize{
  font-size: 100px;
}

hr.divider {
  max-width: 3.25rem;
  border-width: 0.2rem;
  border-color: #f4623a;
}
.masthead {
  padding-top: 10rem;
  padding-bottom: calc(10rem - 4.5rem);
  background: linear-gradient(to bottom, rgba(16, 40, 77, 0.8) 0%, rgba(20, 96, 211, 0.8) 100%), url("assets/bg-masthead1.jpg");  
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: scroll;
  background-size: cover;
}
masthead h1 {
  font-size: 2.25rem;
}
@media (min-width: 992px) {
  .masthead {
    height: 100vh;
    min-height: 40rem;
    padding-top: 4.5rem;
    padding-bottom: 0;
  }
  .masthead p {
    font-size: 1.15rem;
  }
  .masthead h1 {
    font-size: 3rem;
  }
}
@media (min-width: 1200px) {
  .masthead h1 {
    font-size: 3.5rem;
  }
}

</style>
