<template>
  <div class="card-container">
    <h1>Calculate</h1>
    <div class="input-group-container">
      <label for="mileage">Car mileage <span class="unit">(l/100km)</span>: </label>
       <select v-model="mileage" id="mileage" name="mileage">
        <option value="" selected disabled hidden>Choose</option>
        <option value=3>3</option>
        <option value=3.5>3.5</option>
        <option value=4>4</option>
        <option value=5>5</option>
     </select>
      <div class="input-item">
        <label for="distance">Distance</label>
        <input type="number" min="1" class="input-item-field" id="distance" placeholder="Distance in km" v-model="distance" />
      </div>
      <div class="input-item">
        <label for="speed1">Speed 1</label>
        <input type="number" min="1" class="input-item-field" placeholder="Speed 1 in km/hr" v-model="speed1" id="speed1" />
      </div>
      <div class="input-item">
        <label for="speed2">Speed 2</label>
        <input type="number" min="1" class="input-item-field" id="speed2" placeholder="Speed 2 in km/hr" v-model="speed2" />
      </div>
    </div>
    <p>Total consumption 1: {{totalConsumption1}} litres</p>
    <p>Total consumption 2: {{totalConsumption2}} litres</p>
    <p class="result-text">Consumption Difference: {{consumptionDifference}} litres</p>
    <div>Total time 1:
      <span v-if="time1 && speed1 && speed2">{{formatTime(time1)}}</span> 
    </div>
    <div>Total time 2:
      <span v-if="time1 && speed1 && speed2">{{formatTime(time2)}}</span> 
       </div>
    <div class="result-text">Time saved: 
      <span v-if="speed1 && speed2">{{formatTime(time1-time2)}}</span> 
      </div>
  </div>
</template>

<script>
export default {
  name: 'Car',
  data: () => {
    return {
      distance: null,
      speed1: null,
      speed2: null,
      slope: 1.009,
      mileage: "",
    }
  },
  computed: {
    fuelperKm: function (){
      return this.mileage/100
    },
    totalConsumption1: function (){
      return this.totalConsumption(this.speed1)
  },
    totalConsumption2: function (){
      return this.totalConsumption(this.speed2)
  },
    consumptionDifference: function(){
      const difference = this.totalConsumption2 - this.totalConsumption1;
      return Math.round((difference + Number.EPSILON) * 100) / 100;

    },
    time1: function (){
       return this.time(this.speed1);

  },
  time2: function (){
    return this.time(this.speed2);
  }

},
methods: {
  totalConsumption: function (speed){
    const fuelconsumed = this.fuelperKm*this.distance*Math.pow(this.slope, speed)
    return Math.round((fuelconsumed + Number.EPSILON) * 100) / 100;
  },
  time: function (speed){
    return this.distance/speed;
  },
  formatTime: function (time){
     const hours = Math.floor(time);
    const minutes = Math.round((time*60) % 60);
    return `${hours}hrs ${minutes}mins`
  }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.card-container {
  padding: 30px;
  border: 1px solid;
  border-radius: 10px;
  box-shadow: 3px 3px 5px 6px #ccc;
}
.input-item {
  margin: 15px 0 0 0;
}
.input-item-field {
  margin-left: 10px;
  height: 30px;
}
select {
  font-size: 16px;
}
.result-text {
  font-weight: bold;
  font-size: 18px;
}
.unit {
  font-style: italic;
}
</style>
