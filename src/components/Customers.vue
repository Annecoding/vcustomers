<template>
  <div class="customers container">
    <!-- 如果当前alert有内容弹出来  没内容不显示  v-if  添加成功之后传过来相应信息-->
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">用户管理系统</h1>

    <input type="text" class="form-control" placeholder="搜索 🔍 " v-model="filterInput">
    <br>
 
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th></th>
        </tr> 
      </thead>

      <tbody>
        <!-- filterInput 应该遍历搜索的方法  根据名字匹配 -->
        <!-- <tr v-for="customer in customers"> -->
          <tr v-for="customer in filterBy(customers,filterInput)"> 
          <td>{{customer.name}}</td>
          <td>{{customer.phone}}</td>
          <td>{{customer.email}}</td> 
          <td><router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">详情</router-link></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Alert from './Alert'

export default {
  name: 'customers',
  data () {
    return {
        customers:[],
        alert:"",
        filterInput:""
    }
  },
  methods:{
    fetchCustmoers(){
      this.$http.get("http://localhost:3000/users")
                .then(function (response) {
                    //  console.log(response);
                    this.customers = response.body;
                })
    },
    filterBy(customers,value){//value为input的值  filter会遍历数组的所有内容  根据匹配的名称返回整个对象
      return customers.filter(function (customer) {
        return customer.name.match(value);//match方法匹配
      })
    }
  },
  created () {
    if (this.$route.query.alert) {//判断提交是否有内容,就进入这个判断  然后赋值alert
      this.alert = this.$route.query.alert;
    }
    this.fetchCustmoers();
  },
  updated () {//更新的时候也刷新列表
    this.fetchCustmoers();
  },
  components:{
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
