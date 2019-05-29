<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <EmployeeForm @add:employee="addEmployee"/>
    <EmployeeTable
      :employees="employees"
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
    />
  </div>
</template>

<script>
import EmployeeTable from "@/components/EmployeeTable.vue";
import EmployeeForm from "@/components/EmployeeForm.vue";
export default {
  name: "app",
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: "Richard Hendricks",
          email: "richard@piedpiper.com"
        },
        {
          id: 2,
          name: "Bertram Gilfoyle",
          email: "gilfoyle@piedpiper.com"
        },
        {
          id: 3,
          name: "Dinesh Chugtai",
          email: "dinesh@piedpiper.com"
        }
      ]
    };
  },
  methods: {
    addEmployee(employee) {
      let lastId;
      if (this.employees.length > 0) {
        lastId = this.employees[this.employees.length - 1].id;
      } else {
        lastId = 0;
      }
      const id = lastId + 1;
      const newEmployee = { ...employee, id };

      this.employees = [...this.employees, employee];
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter(employee => employee.id !== id);
    },
    editEmployee(id, updatedEmployee) {
      this.employees = this.employees.map(employee =>
        employee.id === id ? updatedEmployee : employee
      );
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<style>
button {
  background: #009435;
  border: 1px solid #009435;
}

.small-container {
  max-width: 680px;
}
</style>