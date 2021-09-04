<template>
  <div>
    <h2>Filter Airports</h2>
    <div class="filters">
      <div class="check-type">
        <ul>
          <li>Small</li>
          <li>Medium</li>
          <li>Large</li>
          <li>Heilport</li>
          <li>Closed</li>
          <li>in your favorites</li>
        </ul>
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
        <tr v-for="airData in airportData" :key="airData.id">
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
    };
  },
};
</script>
