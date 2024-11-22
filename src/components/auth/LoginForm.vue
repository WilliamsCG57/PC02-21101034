<template>
  <div class="container">
    <div class="wrapper">
      <form action="#">
        <h2>Login</h2>
        <div class="input-field">
          <input
            v-model="email"
            type="text"
            placeholder="Email or Phone"
            required
          />
          <label>Enter your email</label>
        </div>
        <div class="input-field">
          <input
            v-model="password"
            type="password"
            placeholder="Password"
            required
          />
          <label>Enter your password</label>
        </div>
        <div class="forget">
          <label for="remember">
            <input type="checkbox" id="remember" />
            <p>Remember me</p>
          </label>
          <a href="#">Forgot password?</a>
        </div>
        <div class="row button">
          <input type="button" value="Login" @click="iniciarSesion" />
        </div>
        <div class="register">
          <p>Don't have an account? <a href="#">Register</a></p>
        </div>
      </form>
    </div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@200;300;400;500;600;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Open Sans", sans-serif;
}

body {
  margin: 0;
  height: 100vh;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: url("https://images.unsplash.com/photo-1477346611705-65d1883cee1e?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D")
    no-repeat center center fixed;
  background-size: cover;
  position: relative;
}

.container::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: -1;
}

.wrapper {
  display: grid;
  gap: 20px; /* Espaciado entre los elementos */
  width: 400px;
  padding: 30px;
  border-radius: 8px;
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

form {
  display: grid;
  gap: 20px; /* Espaciado entre campos del formulario */
}

h2 {
  font-size: 2rem;
  margin-bottom: 20px;
  color: #fff;
}

.input-field {
  position: relative;
  border-bottom: 2px solid #ccc;
  margin: 15px 0;
}

.input-field label {
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  color: #ccc;
  font-size: 16px;
  pointer-events: none;
  transition: 0.15s ease;
}

.input-field input {
  width: 100%;
  height: 40px;
  background: transparent;
  border: none;
  outline: none;
  font-size: 16px;
  color: #fff;
  padding: 5px 0;
}

.input-field input:focus ~ label,
.input-field input:valid ~ label {
  font-size: 0.8rem;
  top: 10px;
  transform: translateY(-120%);
  color: #fff;
}

.forget {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 15px 0;
  color: #fff;
  font-size: 0.9rem;
}

.forget label {
  display: flex;
  align-items: center;
}

.forget label p {
  margin-left: 8px;
}

.wrapper a {
  color: #efefef;
  text-decoration: none;
}

.wrapper a:hover {
  text-decoration: underline;
}

.row.button input[type="button"] {
  background: rgb(255, 255, 255);
  color: #0c0c0c;
  font-weight: 600;
  border: none;
  padding: 12px 20px;
  cursor: pointer;
  border-radius: 3px;
  font-size: 16px;
  border: 2px solid rgba(255, 255, 255, 0.2);
  transition: 0.3s ease;
  width: 100%;
}

.row.button input[type="button"]:hover {
  color: #fff;
  border-color: #fff;
  background: rgba(247, 244, 244, 0.15);
}

.register {
  text-align: center;
  margin-top: 20px;
  color: #fff;
}
</style>

<script>
export default {
  name: "LoginForm",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    iniciarSesion() {
      let endpointURL = "/api/v1/user/signin";
      let user = {
        email: this.email,
        password: this.password,
      };
      this.$api
        .post(endpointURL, user)
        .then((response) => {
          //save response.data in LocalStorage
          localStorage.setItem("userData", JSON.stringify(response.data));
          console.log(JSON.stringify(response));
          this.$q.notify({
            message: "Las credenciales son correctas",
            color: "positive",
            timeout: 5000,
            position: "top",
          });
          this.$router.push("/dashboard/listadoMovies");
        })
        .catch((error) => {
          this.$q.notify({
            message: "Ocurrió un error",
            color: "negative",
            timeout: 5000,
            position: "bottom",
          });
        });
    },
  },
};
</script>
