<script>
import axios from "axios";

export default {
  name: "UserView",
  data() {
    return {
      users: []
    }
  },
  methods: {
    getStudents() {
      axios.get('http://localhost:8080/users/listarDetallado').then(res => {
        this.users = res.data;
        console.log(this.users);
      }).catch(function (error) {
        // handle error on UI site
      })
    },

    deleteUserById(userId) {
      if (confirm('Are you sure, you want to delete this data?')) {
        axios.delete(`http://localhost:8080/users/${userId}`).then(res => {
          this.getStudents();
        }).catch(function (error) {
          // handle error on UI site
        })
      }
    }
  },
  mounted() {
    this.getStudents();
  }


}
</script>

<template>
  <div class="course">
    <div class="card">
      <div class="card-header">
        <h4>
          Usuarios
          <RouterLink to="/users/create" class="btn btn-primary float-end">
            agregar Usuario
          </RouterLink>
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>Nro.</th>
              <th>First Name</th>
              <th>Last Name</th>
              <th>Email</th>
              <th>Age</th>
              <th>fecha Nacimiento</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody v-if="users.length > 0">
            <tr v-for="(user, index) in this.users" :key="index">
              <td>{{ index + 1 }}</td>
              <td>{{ user.firstName }}</td>
              <td>{{ user.lastName }}</td>
              <td>{{ user.email }}</td>
              <td>{{ user.age }}</td>
              <td>{{ user.birthDay }}</td>
              <td>
                <RouterLink :to="{ path: '/users/' + user.id + '/edit' }" class="btn btn-success">
                  Edit
                </RouterLink>&nbsp;
                <button type="button" @click="deleteUserById(user.id)" class="btn btn-danger">
                  Delete
                </button>
              </td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td colspan="7">There are no students</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>