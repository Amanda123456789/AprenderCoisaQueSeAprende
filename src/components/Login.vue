<template>
  <b-container>
    <b-form @submit="onSubmit">
      <b-form-group id="input-group-1" label="Email address:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Senha :" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.password"
          type="password"
          required
          placeholder="Enter password"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="dark">Enviar</b-button>
    </b-form>
    <br>
    <b-card border-variant="light" bg-variant="dark" align="justify">
      <b-card-text>Não possui cadastro? Clique no botão abaixo:</b-card-text>
      <b-button variant="info" to="Cadastro">Cadastrar-se</b-button>
    </b-card>
  </b-container>
</template>

<script>
import { auth } from "@/database";
export default {
  data() {
    return {
      form: {
        email: "teste@gmail.com",
        password: "102030"
      }
    };
  },
  methods: {
    onSubmit(evento) {
      auth
        .signInWithEmailAndPassword(this.form.email, this.form.password)
        .then(user => {
          this.$router.push({ path: "/" });
        })
        .catch(erro => {
          console.log(erro);
        });

      evento.preventDefault();
      //alert(JSON.stringify(this.form));
    }
  }
};
</script>