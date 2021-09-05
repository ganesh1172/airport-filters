<template>
  <div>
    <h2>Filter Airport</h2>
    <div class="filters">
      <div class="check-type">
        <h3>Type</h3>
        <ul>
          <li><input type="checkbox" value="small" />Small</li>
          <li><input type="checkbox" value="medium" />Medium</li>
          <li><input type="checkbox" value="large" />Large</li>
          <li><input type="checkbox" value="heilport" />Heilport</li>
          <li><input type="checkbox" value="closed" />Closed</li>
          <li>
            <input type="checkbox" value="in your favorites" />in your favorites
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
    };
  },
  computed: {
    filteredData() {
      return this.airportData.filter((c) => {
        if (this.searchData == "") return true;
        return c.name.toLowerCase().indexOf(this.searchData.toLowerCase()) >= 0;
      });
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
