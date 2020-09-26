<template>
  <div>
    <b-container class="d-flex justify-content-center">
    <table class="table">
      <tbody class="detail-list">
        <tr>
          <td>ID</td>
          <td>：</td>
          <td>{{ employee.id }}</td>
        </tr>
        <tr>
          <td>Name</td>
          <td>：</td>
          <td>{{ employee.name }}</td>
        </tr>
        <tr>
          <td>Department</td>
          <td>：</td>
          <td>{{ employee.department }}</td>
        </tr>
        <tr>
          <td>Gender</td>
          <td>：</td>
          <td>{{ employee.gender }}</td>
        </tr>
        <tr>
          <td>Birth</td>
          <td>：</td>
          <td>{{ employee.birth }}</td>
        </tr>
        <tr>
          <td>Joined_date</td>
          <td>：</td>
          <td>{{ employee.joined_date }}</td>
        </tr>
        <tr>
          <td>Payment</td>
          <td>：</td>
          <td>{{ employee.payment }}</td>
        </tr>
        <tr>
          <td>Note</td>
          <td>：</td>
          <td>{{ employee.note }}</td>
        </tr>
      </tbody>
    </table>
    </b-container>
    <router-link to="/">
      <b-button variant="outline-info">TOP</b-button>
    </router-link>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      employee: {}
    }
  },
  mounted () {
    axios
      .get(`/api/v1/employees/${this.$route.params.id}.json`)
      .then(response => (this.employee = response.data))
  }
}
</script>

<style>
.detail-list {
  border: solid 1px grey;
  padding: 10px 20px 20px 20px;
  border-radius: 5px;
}
</style>