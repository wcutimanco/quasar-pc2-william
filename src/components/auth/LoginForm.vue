<template>
  <q-layout>
    <q-page-container>
      <q-page class="flex flex-center" q-pa-md style="height: 100vh">
        <q-card-section>
          <h5>Inicio de sesion</h5>
        </q-card-section>

        <q-card-section>
          <q-input
            v-model="emailValue"
            standout="bg-teal text-yellow"
            label="Email"
            outlined
            dense
          />
          <q-input
            v-model="pwdValue"
            type="password"
            standout="bg-teal text-yellow"
            label="Password"
            outlined
            dense
          />
        </q-card-section>

        <q-card-section>
          <q-btn label="login" color="brown" @click="inicioDeSesion"></q-btn>
        </q-card-section>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<style></style>

<script>
export default {
  name: "LoginForm",
  data() {
    return {
      emailValue: "",
      pwdValue: "",
    };
  },
  methods: {
    inicioDeSesion() {
      console.log("Realizo clic en el botón de inicio de sesion");
      console.log("Valor de email: " + this.emailValue);

      let endpointLogin = "/api/v1/user/signin";
      let user = { email: this.emailValue, password: this.pwdValue };
      this.$api
        .post(endpointLogin, user)
        .then((response) => {
          //Respuesta exitosa
          console.log("Respuesta exitosa: " + JSON.stringify(response));
          this.$q.notify({
            message: "Bienvenido a mi sitio web",
            color: "positive",
            position: "bottom",
            timeout: 5000,
          });
          this.$route.push("/peliculas/listado");
        })
        .catch((error) => {
          //Ocurrio un error
          this.$q.notify({
            message: "Usuario incorrecto error",
            color: "negative",
            position: "bottom",
            timeout: 5000,
          });
          console.log("Error en: " + error);
        });
    },
  },
};
</script>
