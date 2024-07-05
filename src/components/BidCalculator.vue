<template>
  <div>
    <h1>Bid Calculation</h1>
    <form @submit.prevent="calculateBid">
      <div>
        <label for="basePrice">Vehicle Base Price:</label>
        <input type="number" v-model="basePrice" id="basePrice" required>
      </div>
      <div>
        <label for="vehicleType">Vehicle Type:</label>
        <select v-model="vehicleType" id="vehicleType" required>
          <option value="Common">Common</option>
          <option value="Luxury">Luxury</option>
        </select>
      </div>
      <button type="submit">Calculate</button>
    </form>
    <div v-if="result">
      <h2>Result</h2>
      <p>Base Price: {{ result.basePrice }}</p>
      <p>Basic Fee: {{ result.basicFee }}</p>
      <p>Special Fee: {{ result.specialFee }}</p>
      <p>Association Fee: {{ result.associationFee }}</p>
      <p>Storage Fee: {{ result.storageFee }}</p>
      <p>Total Cost: {{ result.totalCost }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      basePrice: 0,
      vehicleType: 'Common',
      result: null
    };
  },

methods: {
  async calculateBid() {
    try {
    const response = await axios.post('http://localhost:5004/api/BidCalculation/calculate', {
      BasePrice: this.basePrice,
      VehicleType: this.vehicleType
    }, {
      headers: {
        'Content-Type': 'application/json;charset=UTF-8',
        "Access-Control-Allow-Origin": "*"
      }
    });
    this.result = response.data;
  } catch (error) {
    console.error("There was an error!", error);
  }
  }
}

};
</script>