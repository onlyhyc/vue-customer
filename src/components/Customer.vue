<template>
<div class="container">
  <h1 class="page-header">用户管理系统</h1>
  <input type="text" placeholder="search" class="form-control" v-model="filterSearch">
  <br>
  <alert v-if="alert" :message='alert'></alert>
  <table class="table table-striped">
    <thead>
      <tr>
        <th>姓名</th>
        <th>电话</th>
        <th>邮箱</th>
        <th>其他</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="cust in filterBy(customer,filterSearch)">
        <td>{{cust.name}}</td>
        <td>{{cust.phone}}</td>
        <td>{{cust.email}}</td>
        <td><router-link :to="'/customer/'+cust.id" class="btn btn-default">详情</router-link></td>
      </tr>
    </tbody>
  </table>
  <!-- <button type="button" name="button" @click=fetchCustomer></button> -->
</div>
</template>

<script>
import axios from 'axios'
import Alert from './Alert.vue'
export default {
  'name': 'customer',
  components:{
    Alert
  },
  data() {
    return {
      customer: [],
      alert:"",
      filterSearch:""
    }
  },
  methods: {
    fetchCustomer() {
      this.$http.get('http://localhost:3000/users').then((res) => {
        this.customer = res.data;
        // console.log(this.customer.id);
      })
    },
    filterBy(customer,value){
      return customer.filter((customer)=>{
        return customer.name.match(value);
      });
    }
  },
  created(){
    if(this.$route.query.alert){
      this.alert=this.$route.query.alert;
    }
    this.fetchCustomer()
  },
  // updated(){
  //   this.fetchCustomer()
  // }
}
</script>

<style scoped>
</style>
