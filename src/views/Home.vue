<template>
  <div class="home">
    <Login />
  </div>
</template>

<script>
// @ is an alias to /src
import Login from "./Login";

export default {
  name: "home",
  components: {
    Login
  },
  methods: {
    cickaction() {
      console.log("cickaction");
    }
  }
};
</script>
