<script setup>
import Formik from './components/Formik.vue'
import InputCustom from './components/InputCustom.vue';
</script>

<template>

  <main>
    <div>
      <Formik>
        <InputCustom as="select" name="gender">
          <option value="male">Male</option>
          <option value="female">Female</option>
        </InputCustom>
      </Formik>
    </div>
  </main>
</template>

<style scoped>

</style>
