<template>
  <div id="app">
    <div v-if="hasResult">
        <table border="1">
            <tr>
                <th>employeeId</th>
                <th>firstName</th>
                <th>lastName</th>
                <th>email</th>
                <th>_links</th>
            </tr>
            
            <tr v-for="employee in employees" v-bind:key="employee.employeeId">
                <td>{{employee.employeeId}}</td>
                <td>{{employee.firstName}}</td>
                <td>{{employee.lastName}}</td>
                <td>{{employee.email}}</td>
                <td>{{employee._links}}</td>
            </tr>
           
        </table>
    </div>
    <button v-else v-on:click="searchTerm">Employees Info</button>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      employees: []
    }
  },
  computed: {
    hasResult: function () {
      return this.employees.length > 0
    }
  },
  methods: {
    searchTerm: function () {
      // using JSONPlaceholder
      const baseURI = 'http://localhost:8080';
      this.$http.get(`${baseURI}/employees`)
      .then((result) => {
        console.log(result)
        this.employees = result.data.employees;
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 560px;
}
</style>