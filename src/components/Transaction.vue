<template>
  <div class="wrapper fadeInDown">
    <div id="formContent">
      <!-- Tabs Titles -->

      <legend class="legend">Comprar producto</legend>
      <form v-on:submit.prevent="processTransaction">
        <input
          type="text"
          v-model="createTransaction.name"
          placeholder="Name"
        />
        <br />
        <input
          type="text"
          v-model="createTransaction.category"
          placeholder="Category"
        />
        <br />
        <input
          type="text"
          v-model="createTransaction.brand"
          placeholder="Brand"
        />
        <br />
        <input
          type="number"
          v-model="createTransaction.price"
          placeholder="Price"
        />
        <br />
        <input type="submit" class="fadeIn fourth" value="Crear" />
      </form>
    </div>
  </div>
</template>
<script>
import gql from "graphql-tag";
export default {
  name: "Transaction",
  data: function () {
    return {
      createTransaction: {
        name: "",
        category: "",
        brand: "",
        price: "",
      },
    };
  },
  methods: {
    processTransaction: async function () {
      if (
        localStorage.getItem("token_access") === null ||
        localStorage.getItem("token_refresh") === null
      ) {
        this.$emit("logOut");
        return;
      }
      localStorage.setItem("token_access", "");
      await this.$apollo
        .mutate({
          mutation: gql`
            mutation ($refresh: String!) {
              refreshToken(refresh: $refresh) {
                access
              }
            }
          `,
          variables: {
            refresh: localStorage.getItem("token_refresh"),
          },
        })
        .then((result) => {
          localStorage.setItem("token_access", result.data.refreshToken.access);
        })
        .catch((error) => {
          this.$emit("logOut");
          return;
        });
      await this.$apollo
        .mutate({
          mutation: gql`
            mutation Mutation($productInput: createProductInput!) {
              createProduct(productInput: $productInput) {
                id
                name
                category
                brand
                price
              }
            }
          `,
          variables: {
            productInput: this.createTransaction,
          },
        })
        .then((result) => {
          alert("Transacción Realizada de Manera Correcta, Revise Historial");
        })
        .catch((error) => {
          alert("Saldo Insuficiente o Destino Incorrecto");
        });
    },
  },
};
</script>

<style>

.transaction {
  margin: 0;
  padding: 0%;
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  
}
.container_transaction {
  border: 3px solid #283747;
  border-radius: 10px;
  width: 25%;
  height: 60%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.transaction h2 {
  color: #283747;
}
.transaction form {
  width: 50%;
}
.transaction input {
  height: 40px;
  width: 100%;
  box-sizing: border-box;
  padding: 10px 20px;
  margin: 5px 0;
  border: 1px solid #283747;
}
.transaction button {
  width: 100%;
  height: 40px;
  color: #e5e7e9;
  background: #283747;
  border: 1px solid #e5e7e9;
  border-radius: 5px;
  padding: 10px 25px;
  margin: 5px 0;
}
.transaction button:hover {
  color: #e5e7e9;
  background: crimson;
  border: 1px solid #283747;
}
.principal .items-principal img {
  max-height: 22rem;
  object-fit: cover;
}
</style>