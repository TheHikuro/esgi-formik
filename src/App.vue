<script setup>
import Formik from './components/Formik.vue';
import InputCustom from './components/InputCustom.vue';
import * as yup from "yup";

const initialValues = {
  name: "",
  email: "",
  password: "",
  gender: "male",
  comment: "",
};

const validationSchema = yup.object({
  name: yup.string().required(),
  email: yup.string().email().required(),
  password: yup.string().min(8).required(),
  gender: yup.string().required(),
  comment: yup.string().required(),
});

const onSubmit = (values) => {
  alert("SUCCESS !\n" + JSON.stringify(values, null, 2));
};

</script>

<template v-slot="defaut">
  <div class="main-container">
    <Formik :initialValues="initialValues" :validationSchema="validationSchema" :onSubmit="onSubmit">
      <InputCustom name="name" as='input' label="Name" placeholder="ex: Karl Marques" />
      <InputCustom name="email" as="input" label="Email" placeholder="ex: exemple@myges.fr" />
      <InputCustom name="password" as="input" label="Password" placeholder="ex: Admin(lol)" type="password" />
      <InputCustom name="gender" as="select">
        <option value="male">Male</option>
        <option value="female">Female</option>
      </InputCustom>
      <InputCustom name="comment" as="textarea" placeholder="Comment" />
      <InputCustom name="submit" as="button" type="submit" label="Submit">Submit</InputCustom>
    </Formik>
  </div>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  min-width: 300px;
}

button {
  padding: 0.5rem;
  border: none;
  border-radius: 0.25rem;
  background-color: rgb(0, 255, 102);
  color: rgb(65, 65, 65);
  font-weight: bold;
  cursor: pointer;
}

.main-container {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  gap: 1rem;
  align-items: center;
  width: 100%;
}
</style>
