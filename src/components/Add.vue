<template>
  <div class="container">
    <h1 class="page-header">添加用户</h1>
    <form @submit="addCustomer">
      <div class="well">
        <h4>用户信息</h4>
        <div class="form-grops">
          <label>*姓名</label>
          <input type="text" class="form-control" placeholder="请输入您的姓名" v-model='customer.name' required oninvalid="setCustomValidity('请输入您的姓名');" oninput="setCustomValidity('');">
          <label>*电话</label>
          <input type="text" class="form-control" placeholder="请输入您的电话" v-model='customer.phone' required oninvalid="setCustomValidity('请输入您的电话');" oninput="setCustomValidity('');">
          <label>*邮箱</label>
          <input type="text" class="form-control" placeholder="请输入您的邮箱" v-model='customer.email' required oninvalid="setCustomValidity('请输入您的邮箱');" oninput="setCustomValidity('');">
          <label>学历</label>
          <input type="text" class="form-control" placeholder="请输入您的学历" v-model='customer.edu'>
          <label>毕业学校</label>
          <input type="text" class="form-control" placeholder="请输入您的毕业学校" v-model='customer.college'>
          <label>职业</label>
          <input type="text" class="form-control" placeholder="请输入您的职业" v-model='customer.work'>
          <label>个人简介</label>
          <textarea v-model="customer.introduce" class="form-control" rows="10"></textarea>
        </div>
        <br>
        <button type="submit" class="btn btn-primary">确认添加</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name:'add',
  data(){
    return{
      customer:{}
    }
  },
  methods:{
    addCustomer(e){
      let phoneReg = /^1[34578]\d{9}$/
      let emailReg = /^[a-zA-Z0-9_.-]+@[a-zA-Z0-9-]+(\.[a-zA-Z0-9-]+)*\.[a-zA-Z0-9]{2,6}$/
      //判断电话是否正确
      if(!phoneReg.test(this.customer.phone)){
        alert("请填写正确的电话");
      //判断邮箱是否正确
      } else if (!emailReg.test(this.customer.email)) {
        alert("请填写正确的邮箱");
      } else{
        let newCustmoer = {
          name:this.customer.name,
          phone:this.customer.phone,
          email:this.customer.email,
          edu:this.customer.edu,
          college:this.customer.college,
          work:this.customer.work,
          introduce:this.customer.introduce
        }
        this.$http.post("http://localhost:3000/users",newCustmoer).then((res)=>{
          console.log(res);
        }).then(()=>{
          setTimeout(()=>{
            this.$router.push({path:'/',query:{alert:"用户信息添加成功！"}})
          },1000)
        })
      }


      e.preventDefault();
    }
  }
}
</script>

<style lang="css">
</style>
