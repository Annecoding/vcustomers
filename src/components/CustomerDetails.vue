<template>
  <div class="details container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
        {{customer.name}}
        <span class="pull-right">
            <!-- 根据所传的id编辑对应的内容 -->
            <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">编辑
            </router-link>
            <!-- 点击删除  把本地接口数据删掉 -->
            <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
        </span>
    </h1>
    <ul class="list-group">
        <li class="list-group-item"><span class="glyphicon glyphicon-phone-alt"> 电话：{{customer.phone}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-envelope"> 邮箱：{{customer.email}}</span></li>
    </ul>

    <ul class="list-group">
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk"> 学&nbsp;&nbsp;历：{{customer.education}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-plus"> 毕业学校：{{customer.graduationschool}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk"> 职&nbsp;&nbsp;业：{{customer.profession}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-plus"> 个人简介：{{customer.profile}}</span></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'customerDetails',
  data () {
    return {
        customer:""
    }
  },
   methods:{
    fetchCustmoers(id){//根据id查询详情
      this.$http.get("http://localhost:3000/users/" + id)
                .then(function (response) {
                    console.log(response);
                    this.customer = response.body;
                })
    },
    deleteCustomer(id) {
        this.$http.delete("http://localhost:3000/users/" + id)
        .then(function(response){
            this.$router.push({//删除成功跳转到主页面
                path:"/",
                query:{
                    alert:"用户删除成功！"
                }
            })
        })
    }
  },
  created(){
      this.fetchCustmoers(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>