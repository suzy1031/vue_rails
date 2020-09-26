<template>
  <div>
    <b-form @submit.prevent="$emit('submit')">
      <div v-if="errors.length != 0">
        <ul v-for="e in errors" :key="e">
          <li><font color="red">{{ e }}</font></li>
        </ul>
      </div>
      <b-container class="d-flex justify-content-center">
      <div class="form-block">
        <!-- 従業員名 -->
        <b-form-group id="input-group-1" label="Name" label-for="input-1">
          <b-form-input id="input-1" v-model="employee.name" type="text" required placeholder="Enter Name"></b-form-input>
        </b-form-group>

        <!-- 部署名 -->
        <b-form-group id="input-group-2" label="Department" label-for="input-2">
          <b-form-input id="input-2" v-model="employee.department" type="text" required placeholder="Enter Department"></b-form-input>
        </b-form-group>

        <!-- 性別 -->
        <b-form-group id="input-group-5" label="Gender" label-for="input-5">
          <b-form-select id="input-5" v-model="employee.gender" required :options="options"></b-form-select>
        </b-form-group>

        <!-- 誕生日 -->
        <label for="birth-datepicker">Birth</label>
        <b-form-datepicker id="birth-datepicker" v-model="employee.birth" class="mb-2"></b-form-datepicker>

        <!-- 入社日 -->
        <label for="joined-date-datepicker">Joined_Date</label>
        <b-form-datepicker id="joined-date-datepicker" v-model="employee.joined_date" class="mb-2"></b-form-datepicker>

        <!-- 給与 -->
        <b-form-group id="input-group-3" label="Payment" label-for="input-3">
          <b-form-input id="input-3" v-model="employee.payment" type="number" required placeholder="Enter Payment"></b-form-input>
        </b-form-group>

        <!-- 備考 -->
        <b-form-group id="input-group-4" label="Note" label-for="input-4">
          <b-form-input id="input-4" v-model="employee.note" type="text" placeholder="Enter Note"></b-form-input>
        </b-form-group>
      </div>
      </b-container>

      <b-container class="d-flex justify-content-center">
        <b-button variant="outline-success" type="submit" class="submit-btn">Commit</b-button>
        <router-link to="/">
          <b-button variant="outline-info">BACK</b-button>
        </router-link>
      </b-container>
    </b-form>
  </div>
</template>

<script>
export default {
  props: {
    employee: {},
    errors: ''
  },
  data() {
    return {
      selected: null,
      options: [
        {value: 0, text: 'other'},
        {value: 1, text: 'male'},
        {value: 2, text: 'female'}
      ]
    }
  }

}
</script>

<style>
.form-block {
  border: solid 1px grey;
  padding: 10px 20px 20px 20px;
  border-radius: 5px;
  margin: 75px 0 15px 0;
}

.submit-btn {
  margin: 0 10px 10px 0;
}
</style>