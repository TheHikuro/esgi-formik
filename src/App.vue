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
    <InputCustom name="gender" as="select">
      <option value="male">Male</option>
      <option value="female">Female</option>
    </InputCustom>
    <button type="submit">Submit</button>
  </Formik>
</template>

<style scoped>

</style>
