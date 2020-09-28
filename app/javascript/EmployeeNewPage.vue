<template>
  <div>
    <Header :username='name'></Header>
    <employee-form-pane :errors="errors" :employee="employee" @submit="createEmployee"></employee-form-pane>
    <Footer></Footer>
  </div>
</template>

<script>
import axios from 'axios';

import EmployeeFormPane from 'EmployeeFormPane.vue';
import Header from './organisms/Header'
import Footer from './organisms/Footer'

export default {
  components: {
    EmployeeFormPane,
    Header,
    Footer
  },
  data() {
    return {
      employee: {
        name: '',
        department: '',
        gender: '',
        birth: '',
        joined_date: '',
        payment: '',
        note: ''
      },
      errors: '',
      name: "NEW"
    }
  },
  methods: {
    createEmployee: function() {
      axios
        .post('/api/v1/employees', this.employee)
        .then(response => {
          let e = response.data;
          this.$router.push({ name: 'EmployeeDetailPage', params: { id: e.id } });
        })
        .catch(error => {
          console.error(error);
          if (error.response.data && error.response.data.errors) {
            this.errors = error.response.data.errors;
          }
        });
    }
  }
}
</script>

<style scoped>
</style>