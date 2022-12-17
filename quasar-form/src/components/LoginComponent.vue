<template>
  <div class="q-pa-md mainDiv" align="center">
    <div align="center">
      <q-form
        @submit="onSubmit"
        @reset="onReset"
        autocapitalize="on"
        class="q-gutter-md"
      >
        <q-input
          filled
          standout="text-white"
          v-model="name"
          label="Username *"
          lazy-rules
          :rules="[
            (val) =>
              (val && val.length > 0) || 'Please Enter Username something',
          ]"
        />

        <q-input
          filled
          standout="text-white"
          type="password"
          v-model="age"
          password
          label="Password *"
          lazy-rules
          :rules="[
            (val) => (val !== null && val !== '') || 'Please type your age',
            (val) => (val > 0 && val < 100) || 'Please type a real age',
          ]"
        />

        <q-toggle v-model="accept" label="I accept the license and terms" />

        <div>
          <q-btn label="Submit" type="submit" color="black" />
          <q-btn
            label="Reset"
            type="reset"
            color="black"
            flat
            class="q-ml-sm"
          />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script>
import { useQuasar } from "quasar";
import { ref } from "vue";

export default {
  setup() {
    const $q = useQuasar();

    const name = ref(null);
    const age = ref(null);
    const accept = ref(false);

    return {
      name,
      age,
      accept,

      onSubmit() {
        if (accept.value !== true) {
          $q.notify({
            color: "red-5",
            textColor: "white",
            icon: "warning",
            message: "You need to accept the license and terms first",
          });
        } else {
          $q.notify({
            color: "green-4",
            textColor: "white",
            icon: "cloud_done",
            message: "Submitted",
          });
        }
      },

      onReset() {
        name.value = null;
        age.value = null;
        accept.value = false;
      },
    };
  },
};
</script>

<style scoped>
.mainDiv {
  margin: 25%;
  width: 50%;
  text-align: center;
  border: 5px solid rgb(0, 0, 0);
  border-radius: 15px;
  padding: 10px;
}
</style>
