<template>
  <div>
    <form
      class="relative space-y-3 rounded-md bg-white p-6 shadow-xl lg:p-10 border border-gray-100 m-10">
      <h1 class="text-center text-xl font-semibold lg:text-2xl">Sign Up</h1>
      <p class="text-center pb-4 text-gray-500">
        Already have an account
        <span class="text-blue-600">
          <RouterLink to="/login">Sign in</RouterLink>
        </span>
      </p>

      <div>
        <label class=""> Email Address </label>
        <input
          type="email"
          placeholder="Info@example.com"
          v-model="email"
          class="mt-2 h-12 w-full rounded-md bg-gray-100 px-3 outline-none focus:ring" />
      </div>

      <div>
        <label class=""> Password </label>
        <input
          type="password"
          placeholder="******"
          v-model="password"
          class="mt-2 h-12 w-full rounded-md bg-gray-100 px-3 outline-none focus:ring" />
      </div>
      <div v-show="error">{{ this.errorMessage }}</div>
      <div>
        <button
          @click="signup()"
          type="button"
          class="mt-5 w-full rounded-md bg-blue-600 p-2 text-center font-semibold text-white outline-none focus:ring">
          Sign up
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import app from "@/lib/firebase";
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";

export default {
  name: "SignupView",
  data() {
    return {
      email: "",
      password: "",
      error: null,
      errorCode: "",
      errorMessage: "",
    };
  },
  methods: {
    signup() {
      const auth = getAuth(app);
      createUserWithEmailAndPassword(auth, this.email, this.password)
        .then((userCredential) => {
          this.user = userCredential.user;
          console.log(this.user);
          this.$router.push({ name: "home" });
        })
        .catch((error) => {
          this.errorCode = error.code;
          this.errorMessage = error.message;
          console.log(this.errorCode, this.errorMessage)
        });
    },
  },
};
</script>

<style lang="scss"></style>
