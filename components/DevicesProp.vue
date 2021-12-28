<template>
  <div id="devicesprop">

    <table>
      <tr>
        <th>Device</th>
        <th>ID</th>
        <th>Value</th>
        <th>Date and Time</th>
      </tr>
      <tr>
        <td><span>{{devices.name}}</span></td>
        <td><span>{{devices.id}}</span></td>
        <td><span>{{devices.value}}</span></td>
        <td><span>{{datetime}}</span></td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
  name: 'DevicesProp',
  props: ['devices'],
  data: function () {
    return {
      date: null,
      dt: null
    }
  },
  computed: {
    datetime: function() {
      this.date = new Date(parseInt(this.devices.timestamp))
      this.dt = (this.date.toUTCString().match(/(\d\d:\d\d:\d\d)/)[0] + ' ' + this.date.toDateString() + ' UTC').replaceAll(' ', ' ');
      return this.dt
    }
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
