
<template>
  <div class="container">
    <h2>Bid Calculation</h2>
    <form @submit.prevent="calculateBid" class="bid-form">
      <div class="form-group">
        <label for="basePrice">Vehicle Base Price:</label>
        <input type="number" v-model.number="basePrice" id="basePrice" required>
      </div>
      <div class="form-group">
        <label for="vehicleType">Vehicle Type:</label>
        <select v-model.number="vehicleType" id="vehicleType" required>
          <option :value="0">Common</option>
          <option :value="1">Luxury</option>
        </select>
      </div>
      <div class="form-group">
        <label for="luxuryBasicFeeRate">Luxury Basic Fee Rate:</label>
        <input type="number" v-model.number="luxuryBasicFeeRate" id="luxuryBasicFeeRate" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="commonBasicFeeRate">Common Basic Fee Rate:</label>
        <input type="number" v-model.number="commonBasicFeeRate" id="commonBasicFeeRate" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="luxurySpecialFeeRate">Luxury Special Fee Rate:</label>
        <input type="number" v-model.number="luxurySpecialFeeRate" id="luxurySpecialFeeRate" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="commonSpecialFeeRate">Common Special Fee Rate:</label>
        <input type="number" v-model.number="commonSpecialFeeRate" id="commonSpecialFeeRate" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="luxuryBasicFeeMin">Luxury Basic Fee Min:</label>
        <input type="number" v-model.number="luxuryBasicFeeMin" id="luxuryBasicFeeMin" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="commonBasicFeeMin">Common Basic Fee Min:</label>
        <input type="number" v-model.number="commonBasicFeeMin" id="commonBasicFeeMin" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="luxuryBasicFeeMax">Luxury Basic Fee Max:</label>
        <input type="number" v-model.number="luxuryBasicFeeMax" id="luxuryBasicFeeMax" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="commonBasicFeeMax">Common Basic Fee Max:</label>
        <input type="number" v-model.number="commonBasicFeeMax" id="commonBasicFeeMax" step="0.01" required>
      </div>
      <div class="form-group">
        <label for="storageFee">Storage Fee:</label>
        <input type="number" v-model.number="storageFee" id="storageFee" step="0.01" required>
      </div>
      <button type="submit" class="submit-button">Calculate</button>
    </form>
    <div v-if="result" class="result">
      <h2>Result</h2>
      <p>Base Price: {{ formatCurrency(result.basePrice) }}</p>
      <p>Basic Fee: {{ formatCurrency(result.basicFee) }}</p>
      <p>Special Fee: {{ formatCurrency(result.specialFee) }}</p>
      <p>Association Fee: {{ formatCurrency(result.associationFee) }}</p>
      <p>Storage Fee: {{ formatCurrency(result.storageFee) }}</p>
      <p>Total Cost: {{ formatCurrency(result.totalCost) }}</p>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import '@/assets/BidCalculation.css';

export default {
  data() {
    return {
      basePrice: 0,
      vehicleType: 0,
      luxuryBasicFeeRate: 0.10,
      commonBasicFeeRate: 0.10,
      luxurySpecialFeeRate: 0.04,
      commonSpecialFeeRate: 0.02,
      luxuryBasicFeeMin: 25.00,
      commonBasicFeeMin: 10.00,
      luxuryBasicFeeMax: 200.00,
      commonBasicFeeMax: 50.00,
      storageFee: 100.00,
      result: null
    };
  },
  methods: {
    async calculateBid() {
      try {
        const response = await axios.post('http://localhost:5004/api/BidCalculation/calculate', {
          BasePrice: this.basePrice,
          VehicleType: this.vehicleType,
          LuxuryBasicFeeRate: this.luxuryBasicFeeRate,
          CommonBasicFeeRate: this.commonBasicFeeRate,
          LuxurySpecialFeeRate: this.luxurySpecialFeeRate,
          CommonSpecialFeeRate: this.commonSpecialFeeRate,
          LuxuryBasicFeeMin: this.luxuryBasicFeeMin,
          CommonBasicFeeMin: this.commonBasicFeeMin,
          LuxuryBasicFeeMax: this.luxuryBasicFeeMax,
          CommonBasicFeeMax: this.commonBasicFeeMax,
          StorageFee: this.storageFee
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
    },
    formatCurrency(value) {
      return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(value);
    }
  }
};
</script>
