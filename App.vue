<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <Devices />
    <DevicesProp
      :devices=JSON.parse(message)
    />
    <!--<DevicesProp
      v-bind:devices="{
        load:
        {
          name: 'hello',
          id: '',
          value: '',
          datetime: ''
        },
        blockheight:
        {
          name: '',
          id: '',
          value: '',
          datetime: ''
        },
        pressure:
        {
          name: '',
          id: '',
          value: '',
          datetime: ''
        }
      }"
    />-->
  </div>
</template>

<script>
import Devices from './components/Devices'
import DevicesProp from './components/DevicesProp'

export default {
  name: 'App',
  components: {
    Devices,
    DevicesProp
  },
  data: function() {
    return {
      message: '{"id":"f7cb80bb41552f1ef77c527c83f6f64f","name":"Block Height","value":"326","timestamp":"1640654424614"}'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 60px;
}
</style>
