//获取所有用户信息
http://localhost:3000/

//获取id为1的用户信息
http://localhost:3000/users/1

//获取公司的信息
http://localhost:3000/companies

//获取公司id为3的用户
http://localhost:3000/companies/3/users

//根据公司名字获取信息

//根据公司名称查询数据
http://localhost:3000/companies?name=Apple
//可以根据多个名称查询
http://localhost:3000/companies?name=Apple&name=Google
//根据公司名称分页查询
http://localhost:3000/companies?_page=1&_limit=2
//获取年龄为30的用户
http://localhost:3000/users?age_gte=30
//获取年龄30和四十之间的用户
http://localhost:3000/users?age_gte=20&age_lte=40
//搜索
http://localhost:3000/users?q=na