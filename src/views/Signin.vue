<template>
  <div class="team">
    <v-form ref="form" v-model="vaild" lazy-validation>
      <v-text-field v-model="name" :counter="10" :rules="nameRules" label="Id" required></v-text-field>

      <v-text-field
        v-model="password"
        :append-icon="show1 ? 'visibility' : 'visibility_off'"
        :rules="[rules.required, rules.min]"
        :type="show1 ? 'text' : 'password'"
        name="input-10-1"
        label="Normal with hint text"
        hint="At least 8 characters"
        counter
        @click:append="show1 = !show1"
      ></v-text-field>

      <v-select
        v-model="select"
        :items="items"
        :rules="[v => !!v || 'Item is required']"
        label="Role"
        required
      ></v-select>

      <v-checkbox
        v-model="checkbox"
        :rules="[v => !!v || 'You must agree to continue!']"
        label="Do you agree?"
        required
      ></v-checkbox>

      <v-btn :disabled="!valid" color="success" @click="validate">Validate</v-btn>

      <v-btn color="error" @click="reset">Reset Form</v-btn>

      <v-btn color="warning" @click="resetValidation">Reset Validation</v-btn>
    </v-form>
  </div>
</template>
<script>
export default {
  data: () => ({
    valid: true,
    name: "",
    nameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    show1: false,
    show2: true,
    show3: false,
    show4: false,
    password: "Password",
    rules: {
      required: value => !!value || "Required.",
      //min: v => v.length >= 8 || "Min 8 characters",
      emailMatch: () => "The email and password you entered don't match"
    },
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+/.test(v) || "E-mail must be valid"
    ],
    select: "host",
    items: ["host", "guest"],
    checkbox: false
  }),

  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        this.snackbar = true;
      }
      this.axios
        .post(
          "http://ec2-15-164-103-237.ap-northeast-2.compute.amazonaws.com:3000/signIn",
          {
            id: this.name,
            pwd: this.password,
            radio: 0
          }
        )
        .then(response => {
          console.log(response.data);
          if (response.data.state == 0) {
            alert("login success");
          } else {
            alert("login faild");
          }
        });
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    }
  }
};
</script>
