<template>
  <div id="devicessocket">
    <h1>Devices for Clients</h1>

    <table> <!-- awwwkkk -->
      <tr>
        <th>Device</th>
        <th>ID</th>
        <th>Value</th>
        <th>Date and Time</th>
      </tr>
      <tr>
        <td><span>{{devices.load.name}}</span></td>
        <td><span>{{devices.load.id}}</span></td>
        <td><span>{{devices.load.value}}</span></td>
        <td><span>{{devices.load.datetime}}</span></td>
      </tr>
      <tr>
        <td><span>{{devices.blockheight.name}}</span></td>
        <td><span>{{devices.blockheight.id}}</span></td>
        <td><span>{{devices.blockheight.value}}</span></td>
        <td><span>{{devices.blockheight.datetime}}</span></td>
        <td></td>
      </tr>
      <tr>
        <td><span>{{devices.pressure.name}}</span></td>
        <td><span>{{devices.pressure.id}}</span></td>
        <td><span>{{devices.pressure.value}}</span></td>
        <td><span>{{devices.pressure.datetime}}</span></td>
        <td></td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
  name: 'Devices',
  data: function () {
    return {
      devices: { // make this an array instead of a hash???
        load:
        {
          name: '',
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
        },
      },
      connection: null
    }
  },
  methods: {
    receiveMessage: function(message) {

      var messageJSON = JSON.parse(message);
      var id = messageJSON.id;
      var name = messageJSON.name;
      var value = messageJSON.value;
      var timestamp = messageJSON.timestamp;
      console.log(id+name+value+timestamp);

      // date and time
      var date = new Date(parseInt(timestamp));
      var datetime = (date.toUTCString().match(/(\d\d:\d\d:\d\d)/)[0] + ' ' + date.toDateString() + ' UTC').replaceAll(' ', ' ');
      console.log(datetime);

      switch(name) { // for demo only... perhaps use an array of devices
        case 'Load': // Load
          this.devices.load.name = name;
          this.devices.load.id = id;
          this.devices.load.value = value;
          this.devices.load.datetime = datetime;
          break;
        case 'Block Height': // Block Height
          this.devices.blockheight.name = name;
          this.devices.blockheight.id = id;
          this.devices.blockheight.value = value;
          this.devices.blockheight.datetime = datetime;
          break;
        case 'Pressure': // Pressure
          this.devices.pressure.name = name;
          this.devices.pressure.id = id;
          this.devices.pressure.value = value;
          this.devices.pressure.datetime = datetime;
          break;
        default:
          // nothing
      }
    }
  },
  created: function() {

    console.log('websocket server: starting...')
    //this.connection = new WebSocket('wss://echo.websocket.org')
    this.connection = new WebSocket('ws://localhost:3000')
    this.connection.onopen = function(event) {
      console.log(event)
      console.log('websocket server: connected')
    }
    this.connection.onmessage = function(event) {
      console.log(event)
      console.log('websocket server: received message')
      // had this worked, we would receive an event object with the attribute data which would contain the JSON string
      this.receiveMessage(event.data);
    }

    // put some sample JSON messages here for demostration as websocket not working:(
    this.receiveMessage('{"id":"f19dbf2edb3a0bd74b0524d960ff21eb","name":"Load","value":"999","timestamp":"1640589983863"}')
    this.receiveMessage('{"id":"a78578c428179b490a0461e76ba5f319","name":"Pressure","value":"363","timestamp":"1640589866619"}')
    this.receiveMessage('{"id":"a78578c428179b490a0461e76ba5f319","name":"Pressure","value":"562","timestamp":"1640589867314"}')
    this.receiveMessage('{"id":"f7cb80bb41552f1ef77c527c83f6f64f","name":"Block Height","value":"177","timestamp":"1640589867815"}')
    this.receiveMessage('{"id":"f19dbf2edb3a0bd74b0524d960ff21eb","name":"Load","value":"440","timestamp":"1640589868316"}')
    this.receiveMessage('{"id":"f7cb80bb41552f1ef77c527c83f6f64f","name":"Block Height","value":"975","timestamp":"1640654430613"}')

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body, table {
    font-family: "Lucida Console", "Courier New", monospace;
  }
  body {
    padding: 32px;
  }
  h1 {
    /*margin: 0;*/
  }
  table {
    border-collapse: collapse;
  }
  tr {
    border: 1px solid grey;
  }
  td, th {
    padding: 8px 8px;
  }
</style>
