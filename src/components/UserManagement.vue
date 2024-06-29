<template>
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-6">
          <div class="mb-3">
            <label for="name" class="form-label">Name :</label>
            <input v-model="name" type="text" class="form-control" id="name">
          </div>
          <div class="mb-3">
            <label for="email" class="form-label">Email :</label>
            <input v-model="email" type="email" class="form-control" id="email">
          </div>
          <button @click="saveUser" class="btn btn-success">Save</button>
          <button @click="updateUser" class="btn btn-primary">Update</button>
        </div>
        <div class="col-md-6">
          <h4>List of Users</h4>
          <div v-for="user in users" :key="user.email" class="card mb-3">
            <div class="card-body">
              <h5 class="card-title">{{ user.name }}</h5>
              <p class="card-text">{{ user.email }}</p>
              <button @click="chooseUser(user)" class="btn btn-primary">Choose</button>
              <button @click="removeUser(user)" class="btn btn-danger">Remove</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        users: [
          { name: 'Cinder Ella', email: 'example@gmail.com' }
        ],
        selectedUser: null
      }
    },
    methods: {
      saveUser() {
        if (this.name && this.email) {
          this.users.push({ name: this.name, email: this.email });
          this.name = '';
          this.email = '';
        }
      },
      updateUser() {
        if (this.selectedUser) {
          this.selectedUser.name = this.name;
          this.selectedUser.email = this.email;
          this.name = '';
          this.email = '';
          this.selectedUser = null;
        }
      },
      chooseUser(user) {
        this.selectedUser = user;
        this.name = user.name;
        this.email = user.email;
      },
      removeUser(user) {
        this.users = this.users.filter(u => u !== user);
      }
    }
  }
  </script>
  
  <style>
  .container {
    max-width: 800px;
  }
  </style>
  