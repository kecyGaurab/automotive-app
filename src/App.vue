<template>
<div class="navbar-container">
  <nav class="navbar">
    Compare fuel efficiency
  </nav>
</div>
<div class="container">
    <Car class="car" name="CAR A" mileage='3'/>
    <Car class="car" name="CAR B" mileage='3.5'/>
    <Car class="car" name="CAR C" mileage='4'/>
  </div>
</template>

<script>
import Car from './components/Car.vue'

export default {
  name: 'App',
  components: {
    Car
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.container {
  display: flex;
  justify-content: space-evenly;
  flex-direction:row;
}
.car {
  align-items: center;
}
.navbar {
  font-size:40px;
  font-weight: bold;
  color: white;
  padding: 15px;
}
.navbar-container{
  background-color:black;
  margin-bottom: 60px;
}
</style>
