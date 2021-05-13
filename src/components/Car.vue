<template>
  <div class="card-container">
    <h1>{{name}}</h1>
    <h4>{{mileage}}</h4>
    <p>Total consumption1: {{totalConsumption1}}</p>
    <p>Total consumption2: {{totalConsumption2}}</p>
    <div>Time1:
      <span v-if="time1 && speed1 && speed2">{{formatTime(time1)}}</span> 
    </div>
    <div>Time2:
      <span v-if="time1 && speed1 && speed2">{{formatTime(time2)}}</span> 
       </div>
    <div>Time saved: 
      <span v-if="speed1 && speed2">{{formatTime(time1-time2)}}</span> 
      </div>
    <div class="input-group-container">
      <div class="input-item">
        <label for="distance">Distance</label>
        <input class="input-item-field" id="distance" placeholder="Distance in km" v-model="distance" />
      </div>
      <div class="input-item">
        <label for="speed1">Speed1</label>
        <input class="input-item-field" placeholder="Speed 1 in km/hr" v-model="speed1" id="speed1" />
      </div>
      <div class="input-item">
        <label for="speed2">Speed2</label>
        <input class="input-item-field" id="speed2" placeholder="Speed 2 in km/hr" v-model="speed2" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'card-containerWorld',
  props: {
    mileage: Number,
    name: String,
  },
  data: () => {
    return {
      distance: null,
      speed1: null,
      speed2: null,
      slope: 1.009,
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
  time1: function (){
       return this.time(this.speed1);

  },
  time2: function (){
    return this.time(this.speed2);
   
  }

},
methods: {
  totalConsumption: function (speed){
    return Math.round((this.fuelperKm*this.distance*Math.pow(this.slope, speed)*100/100))
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
</style>
