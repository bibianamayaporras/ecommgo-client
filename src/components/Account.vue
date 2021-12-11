<template>
  <div id="Historial">
    <h2>producto</h2>
    <div class="container-table">
      <table>
        <tr>
          <th>name</th>
          <th>category</th>
          <th>brand</th>
          <th>price</th>
        </tr>
        <tr v-for="transaction in getProducts" :key="transaction.id">
          <td>{{ transaction.name }}</td>
          <td>{{ transaction.category }}</td>
          <td>{{ transaction.brand }}</td>
          <td>${{ transaction.price }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
export default {
  name: "Account",
  data: function () {
    return {
      username: localStorage.getItem("username") || "none",
      getProducts: [],
    };
  },
  apollo: {
    getProducts: {
      query: gql`
        query {
          getProducts {
            id
            name
            category
            brand
            price
          }
        }
      `,
    },
  },
  created: function () {
    this.$apollo.queries.getProducts.refetch();
  },
};
</script>

<style>
#Historial {
  width: 100%;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
}
#Historial .container-table {
  width: 50%;
  max-height: 250px;
  overflow-y: scroll;
  overflow-x: hidden;
}
#Historial table {
  width: 100%;
  border-collapse: collapse;

  border: 1px solid rgba (0, 0, 0, 0.3);
}
#Historial table td,
#Historial table th {
  border: 1px solid #ddd;

  padding: 8px;
}
#Historial table tr:nth-child(even) {
  background-color: #f2f2f2;
}
#Historial table tr:hover {
  background-color: #ddd;
}
#Historial table th {
  padding-top: 12px;
  padding-bottom: 12px;

  text-align: left;
  background-color: #171942;

  color: white;
}
#Historial > h2 {
  color: #283747;
  font-size: 25px;
}
#Historial .container {
  padding: 30px;
  border: 3px solid rgba (0, 0, 0, 0.3);

  border-radius: 20px;

  margin: 5% 0 1% 0;
}
#Historial .container h2 {
  font-size: 25px;

  color: #283747;
}
#Historial .container span {
  color: crimson;
  font-weight: bold;
}
</style>
