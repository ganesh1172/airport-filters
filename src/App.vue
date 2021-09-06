<template>
  <div class="container">
    <h1 class="title-logo">Filter <span>airports</span></h1>
    <div class="filters">
      <div>
        <h3>Type</h3>
        <ul class="check-type">
          <li v-for="type in typeList" :key="type">
            <input type="checkbox" :value="type" v-model="checkType" />{{
              type
            }}
          </li>
        </ul>
      </div>
      <div class="search-type">
        <h3>Filter by search</h3>
        <input
          type="text"
          placeholder="Enter airport name..."
          v-model="searchData"
        />
      </div>
    </div>
    <div class="horizontal-scroll">
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>ICAO</th>
            <th>IATA</th>
            <th>Elev.</th>
            <th>Lat.</th>
            <th>Long.</th>
            <th>Type</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="airData in filteredData" :key="airData.id">
            <td>{{ airData.name }}</td>
            <td>{{ airData.icao }}</td>
            <td>{{ airData.iata }}</td>
            <td>{{ airData.elevation }}</td>
            <td>{{ airData.latitude }}</td>
            <td>{{ airData.longitude }}</td>
            <td>{{ airData.type }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import data from "./data.json";
export default {
  data() {
    return {
      airportData: data,
      searchData: "",
      checkType: [],
      typeList: [
        "small",
        "medium",
        "large",
        "heliport",
        "closed",
        "in your favorites",
      ],
    };
  },
  computed: {
    filteredData() {
      return this.airportData
        .filter((airdata) =>
          airdata.name.toLowerCase().includes(this.searchData.toLowerCase())
        )
        .filter(
          (airdata) =>
            !this.checkType.length || this.checkType.includes(airdata.type)
        );
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}
.container {
  margin: 2rem;
  padding: 2rem;
  background-color: #fbfcfc;
}

.title-logo {
  font-size: 3.5vmax;
}

.title-logo span {
  color: #e5e8e8;
}

.filters {
  display: flex;
  justify-content: space-between;
  margin: 1.5rem 0;
  align-items: center;
}

ul li {
  list-style-type: none;
  display: inline-block;
}

.check-type {
  padding-top: 0.7rem;
}

.check-type li {
  margin-right: 1rem;
  text-transform: capitalize;
  font-size: 1.1rem;
}

input[type="checkbox"] {
  width: 1rem;
  height: 1rem;
  margin-right: 0.5rem;
  color: #000;
}

.search-type input {
  border: none;
  border-bottom: 3px solid;
  font-size: 1rem;
  margin-top: 0.6rem;
  outline: none;
  width: 100%;
  height: 2rem;
}

.horizontal-scroll {
  overflow: hidden;
  overflow-x: auto;
  clear: both;
  width: 100%;
}

table {
  min-width: rem-calc(640);
  width: 100%;
  border-collapse: collapse;
}

table td,
table th {
  padding: 1rem;
  border: none;
}

table th {
  background-color: #e5e8e8;
  text-align: left;
  font-size: 1.2rem;
}

tbody tr:nth-child(odd) {
  background-color: #f4f6f6;
}

tbody tr:hover {
  background-color: #e5e8e8;
}

@media screen and (max-width: 768px) {
  .container {
    margin: 1rem;
    padding: 1rem;
  }
  .filters {
    display: block;
  }
  .search-type {
    margin-top: 1rem;
    width: 100%;
  }
}
</style>
