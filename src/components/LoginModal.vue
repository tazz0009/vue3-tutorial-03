<template>
  <div>
    <section
      @click="close"
      class="z-20 h-screen w-screen bg-gray-500 fixed top-0 opacity-50"
    ></section>
    <div class="absolute inset-0">
      <div class="flex h-full">
        <div class="z-30 m-auto bg-white p-2 rounded shadow w-1/3">
          <div class="p-2 border">
            <h1 class="text-xl text-center">Login</h1>
            <GoogleLogin @close-login-from-google="close" />
            <p class="m-5 text-center">Or</p>
            <form class="p-2 my-2" @submit.prevent="submit">
              <div class="my-4">
                <label>Email or Username</label>
                <input
                  v-model="email"
                  class="rounded shadow p-2 w-full"
                  placeholder="Enter your email or username"
                  ref="emailRef"
                />
              </div>
              <div class="my-4">
                <label>Password</label>
                <input
                  v-model="password"
                  class="rounded shadow p-2 w-full"
                  type="password"
                  placeholder="Enter your password"
                />
              </div>
              <div class="my-4">
                <button
                  type="submit"
                  class="w-full rounded shadow bg-gradient-to-r from-blue-800 to-indigo-800 text-white p-2"
                >
                  <span v-if="isLoading">
                    Loading...
                  </span>
                  <span v-else>
                    Login
                  </span>
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "../utilities/firebase";
import GoogleLogin from "./Login/GoogleLogin";

export default {
  components: { GoogleLogin },
  data() {
    return {
      email: "",
      password: "",
      isLoading: false,
    };
  },
  methods: {
    submit() {
      this.isLoading = true;
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(() => {
          this.email = "";
          this.password = "";
          this.close();
          this.isLoading = false;
        })
        .catch(() => {
          this.isLoading = false;
        });
    },
    close() {
      this.$emit("close-login");
    },
    loginWithGoogle() {
      var provider = new firebase.auth.GoogleAuthProvider();
      firebase
        .auth()
        .signInWithPopup(provider)
        .then(() => {
          this.close();
        })
        .catch(() => {});
    },
  },
  mounted() {
    this.$refs.emailRef.focus();
  },
};
</script>

<style></style>
