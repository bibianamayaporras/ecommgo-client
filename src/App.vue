<template>
  <div id="app" class="app">
    <div class="header">
      <h1>Ecommgo</h1>

      <section class="encabezado-busqueda">
        <div>
          <input
            id="barra-busqueda"
            class="busc"
            type="text2"
            v-model="informacion"
            placeholder="Buscar productos"
          />
          <button class="btn btn-buscar" >
            <i class="bx bx-search">
              <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAAAXNSR0IArs4c6QAAAeRJREFUSEvllu0tRFEQht+tABWgAlSAClABOqACVIAKUMHqABXQASpABeSROTI593wuN/vDSTab7J25z8y8M3N2ojmdyZy46gFvSVqTtCjpXdKTpIdZA6+BVySdSDrIAAjgVtKZpJeeIErgI0nnHS/D/rLVPge+lrTvXnJjmd1bmSk3pd+N7PA7bIGnwD7TV3s5eubOugW1bAbHki5q8BiMps/mBJSXoiOHLHckYRMayz/jtwBfrWkeg32JNwwAlCrQZMDDAXrqdCXIR3uINLmG/DaJwZ8Zx1hzX0lf2mBHUEulcnswzXJnxnumm/dFN5qL8aGpgCyYFFSHceL3qTltm32S78G+qYg26JcL3ENCoEjx1tJkHoxe6JiSIAfHh0Ml+HCCXCyV8Hzg/5uMU8H4jFNy/fj0aFzqlfDMl99PRTFjHqIrDVMdh0wUvvuL90DrHLdk6+e4qG+qifzmYjwoV627eQ/asjzw/7Dvol9tVwOnSWq7mtkFymmSqfV2QjsWBxc/mZDhpi2M1GrkhsIne/7qPqa8BOav0iK85R8IS4AxodtTh0ZinVIJsr9yRll4DexB7HI6lzKjOfqntG+C94BbRirYVOFjgQnAwwclHxMc4HwPOnxs8Ezj1KNpt+3/y/gLRZhwH/pUPqMAAAAASUVORK5CYII="/>
            </i>

            <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAAAXNSR0IArs4c6QAAAbRJREFUSEvNlrkyREEUhr+R254AoQiR0PIEPAESSkRIhIiQSJHgCXgCSygjEuIJbDnqn+q5dWqq+3b3rVbjVE3VLOee72x/97TokbV6xOVfgEeBEdOBu7/shq14F9gxsHdgDnj4iwTqwOLdOnhxtgWr1XrJFoAN915VK4GiFlquIeDNkS6A5aJUqN3qc2DJAWcLgD/svtTJSbCbAkAbYhG40hcxHWujJwrCVwB1MgrWbM8ceK/hkkmmMy7GMCCZRsFashdgsKG0gksaa7WSOzTSGnOJpHbfdqyab0rF8pG2nx3pCNhMpbot1o68mjOi/XhKxZ0TTHPSfFR1e04Rq004FayT7NKBqs2MgGtHlAoWQ0um20sSm4qVa/wfgclu/xywvb20NEokZAKpYpm3QzlgK42EgiuXSrv2oRxwt7RS4EEV5IIFy7kwgtdpE/AqoLYfA1+esvuBdSe501BbcsH7wJYLpptr3hP42vxrOQC2ffBcsA36A/R5gn6bgymUXPLJ1YmvNp+4D2rjmges3+Un0+/edudWrGDjwABwX7PW08An8FRqxikSSvJpUnFS4JhTz8C/k1JKHx+tqHMAAAAASUVORK5CYII="/>
          </button>
        </div>
        <!-- <a href="#">
                        <i class='bx bx-help-circle ayuda'></i>
                    </a> -->
      </section>
      <nav>
        <button v-if="is_auth" v-on:click="loadHome">Inicio</button>
        <button v-if="is_auth" v-on:click="loadAccount">Productos</button>
        <button v-if="is_auth" v-on:click="loadTransaction">
          Comprar 
        </button>
        <button v-if="is_auth" v-on:click="logOut">Cerrar Sesión</button>
        <button v-if="!is_auth" v-on:click="loadLogIn">Iniciar Sesión</button>
        <button v-if="!is_auth" v-on:click="loadSignUp">Registrarse</button>
      </nav>
    </div>

    <div class="main-component">
      <router-view
        v-on:completedLogIn="completedLogIn"
        v-on:completedSignUp="completedSignUp"
        v-on:logOut="logOut"
      >
      </router-view>
    </div>

    <div class="footer">
      
      <h2>Redes Sociales
      <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAAAXNSR0IArs4c6QAAAc1JREFUSEvFlu0xBUEQRe+LABEgAkSACBABGSgRIAIlAkSACBABGSADIqCO2t2aHT09PfPn9a/3Mbunb3/OQkuyxZK46gHvSVqRtD04/SbpS9JLi4goGMippENJqwUA8AdJ15JwxrUaGMiVpJPai7L/byWdDZEwH/XAqLyXtNEIHY9/SDoqqS+BgT45YY36Qvj3LbgFJryvQaWfQ14BjEbx7SbfUb6Th90Ck5/jgCSK6MLII7+dZ8/f5XWSgwkxamtG66DMMgvMuU1JqP+zHBxVS9HQOqnhyM+gzOqCmeocTK4YDjUjZ2mv4sRB5SHevWYpxmMqOWK5wyiNGBX+nIeaqUTfRqwXPKUofUGpKCxHesGXQyfMissDe1WcO+bl2wRTiTeFOLeAKbqtwnvMUHvF1QL2Cm3qhmg70fj0+GiELDXSNAL5bNl3Ovt7B0hPcbkDhBX4HuinHrA7MmFGplAruLokALMWqcx1R3kLmNXJ8klXZ/Gyx0FGW2luR8EUFN3y7w5Wu/oQdkt5BIxSxrB58Ytc9mijfPPUwI/DepyFN01dDTyepdrpTxQQfgtMWIkQ56aFX6qTKDh9nvzn4bN+c7uyBxxo8/qRpYF/ATESYx8MOAMfAAAAAElFTkSuQmCC"/>
      <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAAAXNSR0IArs4c6QAAAapJREFUSEvtlv0xBEEQxd9FQAZkgAgQASJwIkAEiAARIAJE4GRABkIgAuqnerbm5mZnenaV++e6auvu6t706379MTvRkmyyJF6tiP9N+b+Qel3SqaQ9ez4k3Uu6lfRpmWza9/B7ocY4eZR0FB0qqYDDF0l8phYCOJT0ZUF1mDRjQBA/GXlN+pmk3QroXRJ+CQ78r6XEl5Iu7D9A55LeehwjLdnWDHnhAd/5SolzzggmrlcgOpN0XWONZJ5LINdc3xlnRI38PK9W/1idEv+VJLBzliOeSrpzZELz5JoqPeoiRr4NSdtpFzoC6YOc2HgVM/Y2TEscO7kGTaVmjpFwrcVzAcv84nPBxtTYE9uzzbCLGBA1phMPPN4LmP14acS4vl1Nk0FKzYcaY9d7vo+YMWHgx9Q621Qhi9LthNyszSHkrNqbklS1a5GOZKEQxLFT8wc7U4R7iLk0qLnHXKQ4ionJbsvmjgzD9srOYRIF80pwvAC4LHc7MUa1OzY4hxAyznRvFx7mUleH2pJxCIRLHQK2W7itPDzuBTLIWcuhWnO1+GrCroib5BoD/gFW7UcfC0psiQAAAABJRU5ErkJggg=="/>
      <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAAAXNSR0IArs4c6QAAAeNJREFUSEvNlrsuRUEUhr/zBHgCl4YOlUZBoiKChJ5egopQIJFIVCQeQE/iEhoNolFSigJPgDeQP1mT7DNmZl9sOSY5yd5nr5lv//+svWY1aNFotIjLvwd3AZ0F3XkH3vJiU4rbgU1gHtB1mfEJHAHbgK5/jBh4BDitAPQBgs4At/6DEFjqXmuAOpZsH/SVh8D7wFIZX73YJ7vvz/x/ACxn40Jg2dNWESzogM19BBxcqrtTYNn8kQO9s8Rxmat8mDaIYLJVIwvWfUfWbl+xFrlJgBcMGgrZsq9ALyTXnHIXO5pNsjJgB+0D5oBhW/EeOAaeAQcPvVglsOyVG73AITDmrXwNLAIvVjxCxaYSeAVQtm8AO5GtWAd2E6orgd2kK2A8Ar4ApizRVHz88SvwJTARAZ8bVBleG9hZvWZ2htirwF7dVrsC0GN7PemRpVaVSXH61ZZc4jjVqkCzwJDBH4ATA6bKbaU9dgKlSnXXH+4IbarHXlASXKRkykopU0lUvCqUzmw1C6mRLJmaGNujnHWTj9WVNL3YXxyLoTcodCzKPtlYtMfKc0JqtR1NLVCs9VHgWQ3wLysqhVofp0DKddqoEpVVL6CaPc0v1eyFPhf/fI1Z7IpIcgv+fUOfl0Cln7dM8Tdp5m0fVyF0JgAAAABJRU5ErkJggg=="/>
      <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAAAXNSR0IArs4c6QAAATFJREFUSEvtVu0RwUAU3FSACuiADtABHeiADlCBEugAFaADHaADJZjNXMzlhGxO4vLDm8kkmdn3Nvs+7iVCIIsC8eJP/LPM1y7VAwB9Sz7fVbsC4EW7AzgDOLnOruIegC2Ajsoi4kg+tj7opauPjlIxrgRj7GGCtBVT5UUK4Q9qmfSnFLOOB/+YkicVU3mKeAJgLbjvTQ90BawLYZ13LvECwFwItgRA7MzcG4JPAkl8U4qLEjNY05BPRfLSiBM+NuZGmIhKiNkfeQdNacRMNdPMMilWCjGnYGXqrJASk0msjhPHgTXl8VrUMuc42AES7Mhk2qpcElyNz67PWousYbto8XLwNwAjs5tj6Ls/EH6ZPZNsJI6OavEiMMZn+/0jsUrgjavdP5e3EtXxr1jN1Ne4B323OB8cG9DtAAAAAElFTkSuQmCC"/>
       </h2>       
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  computed: {
    is_auth: {
      get: function () {
        return this.$route.meta.requiresAuth;
      },
      set: function () {},
    },
  },
  methods: {
    loadLogIn: function () {
      this.$router.push({ name: "logIn" });
    },
    loadSignUp: function () {
      this.$router.push({ name: "signUp" });
    },
    completedLogIn: function (data) {
      localStorage.setItem("username", data.username);
      localStorage.setItem("token_access", data.token_access);
      localStorage.setItem("token_refresh", data.token_refresh);
      alert("Autenticación Exitosa");
      this.loadHome();
    },
    completedSignUp: function (data) {
      alert("Registro Exitoso");
      this.completedLogIn(data);
    },
    loadHome: function () {
      this.$router.push({ name: "home" });
    },
    loadAccount: function () {
      this.$router.push({ name: "account" });
    },
    loadTransaction: function () {
      this.$router.push({ name: "transaction" });
    },
    logOut: function () {
      localStorage.clear();
      alert("Sesión Cerrada");
      this.loadLogIn();
    },
  },
};
</script>

<style>
body {
  margin: 0 0 0 0;
}

.header {
  margin: 0%;
  padding: 0;
  width: 100%;
  height: 10vh;
  min-height: 100px;

  background-color: #7567f3;
  color: #e5e7e9;

  display: flex;
  justify-content: space-between;
  align-items: center;

  opacity: 0.9;
}

.header h1 {
  width: 20%;
  text-align: center;
}

.header nav {
  height: 100%;
  width: 60%;

  display: flex;
  justify-content: space-around;
  align-items: center;

  font-size: 20px;
}

.header nav button {
  color: #e5e7e9;
  background: #171942;
  border: 1px solid #e5e7e9;

  border-radius: 5px;
  padding: 10px 20px;
}

.header nav button:hover {
  color: #283747;
  background: #e5e7e9;
  border: 1px solid #e5e7e9;
}

.main-component {
  height: 75vh;
  margin: 0%;
  padding: 0%;

  background: #fdfefe;
}

.footer {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 10vh;
  min-height: 100px;

  background-color: #7567f3;
  color: #e5e7e9;

  opacity: 0.9;
}

.footer h2 {
  width: 100%;
  height: 100%;

  display: flex;
  justify-content: center;
  align-items: center;
}
.encabezado-busqueda {
  flex-basis: 80%;
  align-items: center;
  display: flex;
  justify-content: space-between;
}
.btn-buscar {
  height: 3.5 rem;
  margin: 1px;
  border-style: none;
  border-radius: 0.3 rem;
  color: #0e8824;
}
#barra-busqueda {
  width: 600px;
  height: 40px;
  padding: 1.5 rem;
  border-style: none;
  border-radius: 9px;
  margin: 0;
  font-size: medium;
  line-height: initial;
}
.bx {
    font-family: boxicons!important;
    font-weight: 400;
    font-style: normal;
    font-variant: normal;
    line-height: 1;
    text-rendering: auto;
    display: inline-block;
    text-transform: none;
    speak: none;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
.busc{
font-size: x-small;
}
</style>
