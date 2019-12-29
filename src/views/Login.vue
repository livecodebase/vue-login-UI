<template>
  <div>
    <div class="container">
      <div class="wrapper">
        <div class="login-wrap">
          <div class="login-cnt">
            <h1>Log In</h1>
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
            <div class="checkbox-cnt">
              <input type="checkbox" name="checkbox" id="checkbox" />
              <label @click="rememberme" for="checkbox"></label>
              <svg
                v-bind:class="{ hidden: remember }"
                height="20px"
                width="20px"
                viewBox="0 0 20 20"
              >
                <path d="M0 11l2-2 5 5L18 3l2 2L7 18z" />
              </svg>
              <span>Keep me logged in</span>
            </div>
            <div class="login-btn">
              <router-link to="/signup">
                <button>Log In</button>
              </router-link>
            </div>
            <div class="signup-cnt">
              <p>
                Don't have an account?
                <router-link to="/signup"> <span>Sign Up</span> </router-link>
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
  name: "Login",
  data() {
    return {
      remember: false,
      quote: "",
      author: "",
      email: "",
      password: ""
    };
  },
  created() {
    axios.get("https://quotes.rest/qod.json?category=inspire").then(res => {
      this.quote = res.data.contents.quotes[0].quote;
      this.author = res.data.contents.quotes[0].author;
    });
  },
  methods: {
    rememberme() {
      this.remember = !this.remember;
    },
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
  min-width: 500px;
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

/* Checkbox  */
.checkbox-cnt {
  display: flex;
  align-items: center;
  position: relative;
  height: 30px;
}
.checkbox-cnt input {
  display: none;
}
.checkbox-cnt label {
  width: 30px;
  height: 30px;
  border: 2px solid #414141;
  position: absolute;
  top: 0;
  left: 0;
  background: #ffffff00;
  z-index: 20;
}
.checkbox-cnt svg {
  position: absolute;
  top: 5px;
  left: 5px;
  z-index: 19;
}

.hidden {
  display: none;
}

.checkbox-cnt span {
  font-size: 20px;
  color: #414141;
  margin-left: 50px;
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
@media screen and (max-width: 1200px) {
  .login-wrap {
    margin-left: 50px;
  }
  .quote-cnt {
    padding: 0px 20px;
  }
  .quote-text {
    font-size: 30px;
  }
}
@media screen and (max-width: 1000px) {
  .wrapper {
    width: 100%;
    display: block;
    padding: 20px;
  }
  .container {
    background-image: none;
    background-color: #f2f2f2;
    height: 100%;
  }
  .login-wrap {
    width: 100%;
    margin: 0px auto;
    margin-top: 50px;
  }
}
@media screen and (max-width: 600px) {
  .login-wrap {
    width: 100%;
    min-width: auto;
  }
  .quote-cnt {
    min-width: 100%;
  }
  .quote-text {
    font-size: 25px;
  }
  .quote-author {
    font-size: 25px;
  }
  .checkbox-cnt span {
    font-size: 17px;
  }
  .signup-cnt p {
    font-size: 17px;
  }
  .login-cnt {
    padding: 20px;
  }
}
</style>
