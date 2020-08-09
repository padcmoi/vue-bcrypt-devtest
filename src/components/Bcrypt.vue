<template>
  <section>
    <div>
      <h1>Test du paquetage Bcrypt avec Vue</h1>
      <ul>
        <li>- Hashage du mot de passe avec hashPassword</li>
        <li>- Verification du mot de passe avec un Boolean</li>
      </ul>
    </div>Entrer un mot de passe:
    <input type="text" v-model="password" />
    <hr />
    <div>
      Mot de passe en clair:
      <strong>{{ password }}</strong>
    </div>
    <div>
      Mot de passe hashé avec bcrypt:
      <strong>{{ hashPassword }}</strong>
    </div>
    <br />
    <div>checkPassword()</div>
    <div>avec le mot de passe {{ password }}-> {{ checkPassword( password, hashPassword ) }}</div>
    <div>avec un mot de passe faux -> {{ checkPassword( 'faux_mot_de_passe', hashPassword ) }}</div>
  </section>
</template>

<script>
import bcrypt from "bcryptjs";

export default {
  data() {
    return {
      password: "123",
    };
  },
  computed: {
    hashPassword() {
      const saltRounds = 10;
      return bcrypt.hashSync(this.password, saltRounds);
    },
  },
  methods: {
    checkPassword(plaintextPassword = "", hash = "") {
      return bcrypt.compareSync(plaintextPassword, hash);
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
}
strong {
  color: tomato;
}
</style>