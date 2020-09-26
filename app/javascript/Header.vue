<template>
  <header class="main-header">
    <h1>{{ username }}</h1>
    <router-link to="/employees/new">
      <b-button variant="light" class="header-button">NEW</b-button>
    </router-link>
  </header>
</template>

<script>
export default {
  data() {
    return {
      // title: "Employee Data"
    }
  },
  props: {
    username:String
  }
}
</script>

<style>
  .main-header {
    width: 100%;
    background: #007bff;
    position: fixed;
    display: flex;
    justify-content: space-between;
  }

  header > h1 {
    color: white;
    padding: 5px 0 0 5px;
  }

  .header-button {
    margin: 10px 5px 10px 0;
  }
</style>