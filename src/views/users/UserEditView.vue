
<script>
import axios from "axios";

export default {
  name: "UserEditView",
  data() {
    return {
      userId: '',
      model: {
        user: {
          username: '',
          password: '',
          firstName: '',
          lastName: '',
          email: '',
          age: '',
          birthDay: ''
        }
      }
    }
  },
  methods: {
    getStudentById(userId) {
      axios.get(`http://localhost:8080/users/detallado/${userId}`).then(res => {
        this.model.user = res.data;
      }).catch(function (error) {
        // handle error on UI site
      })
    },
    editStudent() {
      axios.put(`http://localhost:8080/users/editar/${this.userId}`, this.model.user)
          .then(res => {
            alert('Student was Edited successful');
          }).catch(function (error) {
            // handle error on UI site
      })
    }
  },
  mounted() {
    this.userId = this.$route.params.id;
    this.getStudentById(this.userId);
  }
}

</script>

<template>
    <div class="container mt-5">
      <div class="card">
        <div class="card-header">
          <h4>Edit User</h4>
        </div>
        <div class="card-body">
          <div class="mb-3">
            <label for="">First Name</label>
            <input type="text" v-model="model.user.firstName" class="form-control">
          </div>
          <div class="mb-3">
            <label for="">Last Name</label>
            <input type="text" v-model="model.user.lastName" class="form-control">
          </div>
          <div class="mb-3">
            <label for="">Age</label>
            <input type="text" v-model="model.user.age" class="form-control">
          </div>
          <div class="mb-3">
            <label for="">Email</label>
            <input type="text" v-model="model.user.email" class="form-control">
          </div>
          <div class="mb-3">
           <label for="">Usuario</label>
           <input type="text" v-model="model.user.username" class="form-control">
          </div>
          <div class="mb-3">
           <label for="">Password</label>
           <input type="text" v-model="model.user.password" class="form-control"> 
          </div>
          <div class="mb-3">
            <button type="button" @click="editStudent" class="btn btn-primary">
              Edit
            </button>&nbsp;
            <RouterLink to="/users" class="btn btn-primary">
              Back
            </RouterLink>
          </div>
        </div>
      </div>
    </div>
  </template>


<style lang="scss" scoped>

</style>