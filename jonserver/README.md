//获取所有用户
http://localhost:3000/users

//获取用户id为1的用户
http://localhost:3000/users/1

//获取所有公司
http://localhost:3000/companies

//获取公司id为1的公司
http://localhost:3000/companies/1

//获取公司id为1的所有用户
http://localhost:3000/companies/1/users

//根据公司名字获取信息
http://localhost:3000/companies?name=Apple

//获取一页中只有两条数据
http://localhost:3000/companies?_page=1&_limit=2

//根据公司名称升序asc排序 desc降序
http://localhost:3000/companies?_sort=name&_order=asc

//获取年龄大于等于18的用户
http://localhost:3000/users?age_gte=18

//获取年龄介于18-20(含)的用户
http://localhost:3000/users?age_gte=18&age_lte=20

//根据搜索信息查询
http://localhost:3000/users?q=l
