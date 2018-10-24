<template>
<div class="container">
  <div><router-link to="/" class="btn btn-default">返回</router-link></div>
  <h1 class="page-header">
    {{customer.name}}

    <span class="pull-right">
      <router-link :to="'/edit/'+customer.id" class="btn btn-primary">编辑</router-link>
      <button class="btn btn-danger" @click="deleteCustomer(customer.id)">删除</button>
    </span>
  </h1>
  <ul class="list-group">
    <li class="list-group-item glyphicon glyphicon-earphone
"><span>：{{customer.phone}}</span></li>
    <li class="list-group-item glyphicon glyphicon-envelope"><span>：{{customer.email}}</span></li>
  </ul>
  <ul class="list-group">
    <li class="list-group-item glyphicon glyphicon-education
"><span>：{{customer.edu}}</span></li>
    <li class="list-group-item glyphicon glyphicon-education"><span>：{{customer.college}}</span></li>
    <li class="list-group-item glyphicon glyphicon-briefcase
"><span>：{{customer.work}}</span></li>
    <li class="list-group-item glyphicon glyphicon-pencil"><span>：{{customer.introduce}}</span></li>
  </ul>
</div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'customerDetails',
  data() {
    return {
      customer: ""
    }
  },
  methods: {
    fetchCustomer(id) {
      this.$http.get('http://localhost:3000/users/' + id).then((res) => {
        this.customer = res.data;
        // console.log(this.customer);
      })
    },
    deleteCustomer(id){
      this.$http.delete('http://localhost:3000/users/'+id).then(()=>{
        this.$router.push({path:'/',query:{alert:"用户删除成功！"}})
      })
    }
  },
  created() {
    this.fetchCustomer(this.$route.params.id)
  }
}
</script>

<style lang="css">
</style>
