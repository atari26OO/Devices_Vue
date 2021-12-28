<template>
  <div id="app">
    <!-- Vue single file component with socket connection -->
    <DevicesSocket />
    <br/>
    <!-- Vue single file component with props -->
    <DevicesProp
      v-for="item in items" :key="item.message"
      :devices=JSON.parse(item.message)
    />
  </div>
</template>

<script>
import DevicesSocket from './components/DevicesSocket'
import DevicesProp from './components/DevicesProp'

export default {
  name: 'App',
  components: {
    DevicesSocket,
    DevicesProp
  },
  data: function() {
    return {
      items: [ // just running through sample messages from a list
        { message: '{"id":"a78578c428179b490a0461e76ba5f319","name":"Pressure","value":"562","timestamp":"1640589867314"}' },
        { message: '{"id":"f19dbf2edb3a0bd74b0524d960ff21eb","name":"Load","value":"440","timestamp":"1640589868316"}' },
        { message: '{"id":"f7cb80bb41552f1ef77c527c83f6f64f","name":"Block Height","value":"975","timestamp":"1640654430613"}' }
      ]
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
