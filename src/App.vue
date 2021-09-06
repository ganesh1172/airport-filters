<template>
  <div>
    <h2>Filter Airport</h2>
    <div class="filters">
      <div class="check-type">
        <h3>Type</h3>
        <ul>
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
ul li {
  list-style-type: none;
  display: inline-block;
}

.filters {
  display: flex;
  justify-content: space-around;
}
</style>
