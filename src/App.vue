<template>
<formComponent
    :initialValues="initialValues"
    :validate="validate"
    :onSubmit="handleSubmit"
  >
    <template v-slot="{ values, errors, isSubmitting, handleSubmit }">
      <form @submit.prevent="handleSubmit">
        <label>
          Nom d'utilisateur :
          <input v-model="values.username" type="text" />
          <span v-if="errors.username">{{ errors.username }}</span>
        </label>
        <label>
          Adresse e-mail :
          <input v-model="values.email" type="email" />
          <span v-if="errors.email">{{ errors.email }}</span>
        </label>
        <label>
          Mot de passe :
          <input v-model="values.password" type="password" />
          <span v-if="errors.password">{{ errors.password }}</span>
        </label>
        <button type="submit" :disabled="isSubmitting">S'inscrire</button>
      </form>
    </template>
  </formComponent>
</template>


<script>
import formComponent from "./components/formComponent.vue";

export default {
  components: {
    formComponent
  },
  data() {
    return {
      initialValues: {
        username: "",
        email: "",
        password: ""
      }
    };
  },
  methods: {
    async validate(values) {
      const errors = {};
      if (!values.username) {
        alert(errors.username = "Le nom d'utilisateur est obligatoire.");
      }
      if (!values.email) {
        errors.email = "L'adresse e-mail est obligatoire.";
      }
      if (!values.password) {
        errors.password = "Le mot de passe est obligatoire.";
      }
      if (Object.keys(errors).length) {
        throw errors;
      }
    },
    async handleSubmit(values) {
      alert("Inscription réussie !")
    }
  }
};
</script>

