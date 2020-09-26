<template>
  <div>
    <Header :username='name'></Header>
    <div v-if="errors.length != 0">
      <ul v-for="e in errors" :key="e">
        <li><font color="red">{{ e }}</font></li>
      </ul>
    </div>
    <b-container class="d-flex justify-content-center">
    <table class="table">
      <tbody>
        <tr>
          <th>ID</th>
          <th>name</th>
          <th>department</th>
          <th>gender</th>
          <th>actions</th>
        </tr>
        <tr v-for="e in employees" :key="e.id">
          <td><router-link :to="{ name: 'EmployeeDetailPage', params: { id: e.id } }">{{ e.id }}</router-link></td>
          <td>{{ e.name }}</td>
          <td>{{ e.department }}</td>
          <td>{{ e.gender }}</td>
          <td>
            <b-button variant="outline-danger" @click="deleteTarget = e.id; showModal = true" v-b-modal.modal-1>Delete</b-button>
          </td>
          <td>
            <router-link :to="{ name: 'EmployeeEditPage', params: { id: e.id } }">
              <b-button variant="outline-warning">Edit</b-button>
            </router-link>
          </td>
        </tr>
      </tbody>
    </table>
    </b-container>
    <Footer></Footer>
    <!-- モーダルウィンドウ（デフォルト非表示） -->
    <b-modal id="modal-1" title="BootstrapVue" v-if="showModal" @cancel="showModal = false" @ok="deleteEmployee(); showModal = false;">
      <p class="my-4">Are you sure?</p>
    </b-modal>
  </div>
</template>

<script>
import axios from 'axios';
import Modal from 'Modal.vue'
import Header from './Header'
import Footer from './Footer'

export default {
  components: {
    Modal,
    Header,
    Footer
  },
  data: function () {
    return {
      employees: [],
      showModal: false,
      deleteTarget: -1,
      errors: '',
      name: "Employee Data"
    }
  },
  mounted () {
    this.updateEmployees();
  },
  methods: {
    deleteEmployee: function() {
      if (this.deleteTarget <= 0) {
        console.warn('deleteTarget should be grater than zero.');
        return;
      }

      axios
        .delete(`/api/v1/employees/${this.deleteTarget}`)
        .then(response => {
          this.deleteTarget = -1;
          this.updateEmployees();
        })
        .catch(error => {
          console.error(error);
          if (error.response.data && error.response.data.errors) {
            this.errors = error.response.data.errors;
          }
        });
    },
    updateEmployees: function() {
      axios
        .get('/api/v1/employees.json')
        .then(response => (this.employees = response.data))
    }
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}

.table {
  margin: 10px 0 0 0;
}
</style>