<script setup>
import Formik from './components/Formik.vue';
import InputCustom from './components/InputCustom.vue';
import { ref } from 'vue';
import * as yup from "yup";

const initialValues = ref({
  name: "",
  email: "",
  password: "",
});
const validationSchema = yup.object({
  name: yup.string().required(),
  email: yup.string().email().required(),
  password: yup.string().min(8).required(),
});

</script>

<template v-slot="defaut">
  <Formik :initial-values="initialValues" :validation-schema="validationSchema" :onSubmit="() => console.log('test')">
    <form>
      <InputCustom name="name" label="Name" formtype="" placeholder="Le input custom" />
      <InputCustom name="email" label="Email" formtype="" placeholder="Le input custom" />
      <InputCustom name="password" label="Password" formtype="" placeholder="Le input custom" />
      <button type="submit">Submit</button>
    </form>
  </Formik>
</template>

<style scoped>

</style>
