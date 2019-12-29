<template>
  <div>
    <div class="container">
      <div class="wrapper">
        <div class="login-wrap">
          <div class="login-cnt">
            <h1>Sign Up</h1>
            <div class="input-cnt">
              <input
                @change="inputactive"
                v-model="username"
                type="username"
                name="username"
                id="username"
              />
              <label for="username">Username</label>
            </div>
            <div class="input-cnt">
              <input
                @change="inputactive"
                v-model="email"
                type="email"
                name="email"
                id="email"
              />
              <label for="email">Email Address</label>
            </div>
            <div class="input-cnt">
              <input
                @change="inputactive"
                v-model="password"
                type="password"
                name="password"
                id="password"
              />
              <label for="password">Password</label>
            </div>
            <div class="login-btn">
              <button>Sign Up</button>
            </div>
            <div class="signup-cnt">
              <p>
                Already have an account!
                <router-link to="/login"> <span>Log In</span> </router-link>
              </p>
            </div>
          </div>
        </div>
        <div class="quote-wrap">
          <div class="quote-cnt">
            <img
              height="200px"
              width="200px"
              src="../assets/quotation-mark.svg"
              alt="quotation-mark"
            />
            <div class="quote">
              <p class="quote-text">{{ this.quote }}</p>
              <div class="divider"></div>
              <div class="quote-author">{{ this.author }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Signup",
  data() {
    return {
      remember: false,
      username: "",
      email: "",
      password: "",
      quote: "",
      author: ""
    };
  },
  created() {
    axios.get("http://quotes.rest/qod.json?category=inspire").then(res => {
      this.quote = res.data.contents.quotes[0].quote;
      this.author = res.data.contents.quotes[0].author;
    });
  },
  methods: {
    inputactive(e) {
      if (e.target.value === "") {
        e.target.classList.remove("inputactive");
      } else {
        e.target.classList.add("inputactive");
      }
    }
  }
};
</script>

<style scoped>
.container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f2f2f2;
  background-image: url("../assets/back.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
.wrapper {
  width: 100%;
  display: flex;
}
.login-wrap {
  width: 50%;
  max-width: 500px;
  background-color: #fff;
  box-shadow: 0 5px 5px 0 rgba(0, 0, 0, 0.05),
    0px 0 20px 0 rgba(167, 171, 255, 0.41);
  display: flex;
  align-items: center;
  padding: 50px 0px;
  margin-left: 100px;
}
.login-cnt {
  width: 100%;
  padding: 50px;
}
.login-cnt h1 {
  font-size: 35px;
  font-weight: bold;
  color: #414141;
  margin-bottom: 10px;
}

/* Input  */
.input-cnt {
  width: 100%;
  position: relative;
  transition: 0.2s ease-in-out;
}
label {
  position: absolute;
  top: 32px;
  font-size: 20px;
  left: 20px;
  color: #b9b9b9;
}
.input-cnt input {
  width: 100%;
  height: 60px;
  font-size: 20px;
  padding-left: 20px;
  margin: 15px 0;
  padding-top: 10px;
  background-color: #f8f8f8;
  border: none;
}
.input-cnt input:focus {
  outline: none;
}
.input-cnt input:focus + label {
  top: 20px;
  font-size: 15px;
  color: #a2a2a2;
  transition: 0.2s ease-out;
}
.inputactive + label {
  top: 20px;
  font-size: 15px;
  color: #a2a2a2;
  transition: 0.2s ease-out;
}
/* Login butoon  */
.login-btn {
  width: 100%;
}
.login-btn button {
  width: 100%;
  height: 50px;
  border: none;
  background-color: #3b3b3b;
  color: #fff;
  font-size: 20px;
  font-weight: 600;
  margin: 15px 0px;
  cursor: pointer;
}
.login-btn button:focus {
  outline: none;
}
.signup-cnt p {
  font-size: 20px;
  font-weight: 600;
  color: #a2a2a2;
}
.signup-cnt span {
  color: #414141;
  cursor: pointer;
}

/* quote  */
.quote-wrap {
  width: 100%;
  display: flex;
  align-items: center;
  padding: 50px 0px;
}
.quote {
  margin-top: -100px;
}
.quote-cnt {
  padding: 50px 0px;
  margin: 0 auto;
  max-width: 600px;
  text-align: center;
}
.quote-text {
  font-size: 35px;
  font-stretch: expanded;
  font-weight: 600;
  text-align: center;
  letter-spacing: 2px;
  color: #3f3f3f;
}
.divider {
  height: 3px;
  background-color: #3b3b3b;
  max-width: 100px;
  margin: 20px auto;
}
.quote-author {
  font-size: 30px;
  font-weight: 600;
  color: #7d7d7d;
}
</style>
