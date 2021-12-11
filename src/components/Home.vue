<template>
  <div class="information">
 
    <div class="details">
           <h1>
      <i>
        ¡Bienvenido
        <span>{{ userDetailById.name }}</span>-<span>{{ userDetailById.lastName }}</span>!
    </i
      ><em>Su <ins>información</ins> es la siguiente</em>
    </h1>
      <h2>
        Nombre de usuario:
        <span>{{ userDetailById.username }}</span>
      </h2>
      <h2>
        Correo electrónico:
        <span>{{ userDetailById.email }}</span>
      </h2>
    </div>
    <main class="contenedor principal">
      <div class="items-principal">
        <img src="@/assets/laptop1.jpg" />
        <h3 class="texto-verde">$150000</h3>
        <p>Tablet, Samsung</p>
        <p>Referencia: Tab 8</p>
      </div>
      <div class="items-principal">
        <img src="@/assets/portatil.jpg" />
        <h3 class="texto-verde">$150000</h3>
        <p>Tablet, Samsung</p>
        <p>Referencia: Tab 8</p>
      </div>
      <div class="items-principal">
        <img src="@/assets/tablet.jpg" />
        <h3 class="texto-verde">$150000</h3>
        <p>Tablet, Samsung</p>
        <p>Referencia: Tab 8</p>
      </div>
      <div class="items-principal">
        <img src="@/assets/portatil.jpg" />
        <h3 class="texto-verde">$150000</h3>
        <p>Tablet, Samsung</p>
        <p>Referencia: Tab 8</p>
      </div>
      <div class="items-principal">
        <img src="@/assets/tablet.jpg" />
        <h3 class="texto-verde">$150000</h3>
        <p>Tablet, Samsung</p>
        <p>Referencia: Tab 8</p>
      </div>
      <div class="items-principal">
        <img src="@/assets/laptop1.jpg" />
        <h3 class="texto-verde">$150000</h3>
        <p>Tablet, Samsung</p>
        <p>Referencia: Tab 8</p>
      </div>
    </main>
  </div>
</template>


<script>
import gql from "graphql-tag";
import jwt_decode from "jwt-decode";
export default {
  name: "Home",
  data: function () {
    return {
      userId: jwt_decode(localStorage.getItem("token_refresh")).user_id,
      userDetailById: {
        username: "",
        name: "",
        lastName:"",
        email: "",
      },
    };
  },
  apollo: {
    userDetailById: {
      query: gql`
        query ($userIdInput: ID!) {
          userDetailById(userIdInput: $userIdInput) {
            username
            name
            lastName            
            email
          }
        }
      `,
      variables() {
        return {
          userIdInput: this.userId,
        };
      },
    },
  },
};
</script>


<style>
.information {
  margin: 30px;
  padding: 5%;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.information h1 {
  font-size: 21px;
  color: #283747;
  text-align: center;
}
.information h2 {
  font-size: 1px;
  color: #283747;
}
.information span {
  color: crimson;
  font-weight: 50px;
}
.details h3 {
  font-size: 25px;
  color: #283747;
  text-align: center;
}
.details h2 {
  font-size: 16px;
  color: #283747;
  text-align: center;
  display: contents;
}
.details {
  border: 3px solid rgba(0, 0, 0, 0.3);
  border-radius: 20px;
  
  margin: -27px 0 0 0;
}

.principal {
  display: -webkit-box;
  flex-wrap: wrap;
  justify-content: space-around;
  margin-top: 0.1rem;
}
.contenedor {
  max-width: 200rem;
  margin: -5px;
  box-sizing: inherit;
  flex-direction: row;
  align-items: stretch;
}
.principal .items-principal {
  display: grid;
  flex-direction: column;
  box-shadow: 1px 1px 5px -16px rgb(87 77 87 / 88%);
  padding: 1.5 rem;
  flex-basis: calc(33% - 2 rem);
  margin-bottom: 1.5 rem;
  border-radius: 10 px 10 px 10 px 10 px;
  background: #fff;
  padding: 30 px;
  width: 30%;
  max-width: 450 px;
  
  padding: 0 px;
  box-shadow: 0px 10px 50px 5px rgb(0 0 0 / 30%); 
margin: 14px;
  
}
.principal .items-principal img {
  max-height: 1rem;
  -o-object-fit: cover;
  object-fit: cover;
  max-width: 40%;
display: block;
margin-left: auto;
margin-right: auto;
  align-items: center;
}
.texto-verde {
  color: #b03a2e;
   text-align: center;
   font-size: 23px;
}
p {
  font-size: 14.8px;
  margin-top: -14px;
  margin-bottom: 0 rem;
   text-align: center;
}
</style>