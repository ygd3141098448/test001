# 1.主界面

`【src/main/resources/templates/html/emp/all.html】`

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>

    <title>My JSP 'all.jsp' starting page</title>
  
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">  
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">

    <link rel="stylesheet" th:href="@{/css/pintuer.css}">
    <link rel="stylesheet" th:href="@{/css/admin.css}">
    <script th:src="@{/js/jquery-3.3.1.min.js}" type="text/javascript"></script>
    <style type="text/css">
     *{
       font-size: 12px;
      }
    </style>

  </head>
  
  <body>
   
  <div class="panel admin-panel">
    <div class="panel-head"><strong class="icon-reorder"> 操作信息管理</strong></div>
    <div class="padding border-bottom">
    </div>
    <table class="table table-hover text-center" id="emp-table">
      <tr>
    
        <th>编号</th>   
        <th>员工姓名</th>
        <th>员工性别</th>
        <th>岗位</th>
        <th align="center">操作</th>   
      </tr>
    </table>
  </div>

</body>
<script>
    $(function(){
        $.get("../gson/empGson",function(data){
            var gsonText = '';
            $(data).each(function(i,n){
                gsonText += '<tr>' +
                    '<td>'+n.eid+'</td>' +
                    '<td>'+n.ename+'</td>' +
                    '<td>'+(n.esex == 1 ? '男':'女')+'</td>' +
                    '<td>'+n.egw+'</td>' +
                    '<td>\n' +
                    '      \t\t\t<div class="button-group">\n' +
                    '\t\t\t\t\t\t<a class="button border-red" href="empControllerUpdate?eid='+n.eid+'">\n' +
                    '\t\t\t<span class="icon-trash-o">\n' +
                    '\t\t\t\t\t</span> 修改</a> \n' +
                    '\t\t\t\t</div>\n' +
                    '\t\t\t</td>' +
                    '</tr>';
            });
            gsonText += '<tr>\n' +
                '       \t\t<td colspan="5" align="center">\n' +
                '\t\t\t\t<a href="empControllerAdd"><button type="button"  ' +
                'class="button border-green" id="checkall"><span class="icon-check"></span> 增加</button></a>\n' +
                '\t\t\t</td>\n' +
                '       </tr>';
            $("#emp-table tbody").append(gsonText);
        });
    });
</script>
</html>

```

点击"增加"按钮将导致浏览器跳转到 `EmpController.java.emp.empControllerAdd`路径

`【com/hjc/springbootmovies/controller/EmpController.java】`

```
package com.hjc.springbootmovies.controller;

import com.hjc.springbootmovies.entity.ModelEmp;
import com.hjc.springbootmovies.service.Impl.EmpServiceImpl;


@Controller
@RequestMapping("emp")
public class EmpController {
    @Autowired
    private EmpServiceImpl empService;
 
    @GetMapping("empControllerAdd")
    public String empAdd(){
        return "html/emp/add";
    }

   
}

```

由 `EmpController.java.emp.empControllerAdd`的 `empAdd`方法处理，并返回"html/emp/add"

# 2.添加员工

`【src/main/resources/templates/html/emp/add.html】`

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>

    <title>My JSP 'add.jsp' starting page</title>
  
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">  
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
    <link rel="stylesheet" th:href="@{/css/pintuer.css}">
    <link rel="stylesheet" th:href="@{/css/admin.css}">
  

  </head>
  
  <body>
    <div class="panel admin-panel">
  <div class="panel-head"><strong><span class="icon-pencil-square-o"></span> 增加员工信息</strong></div>
  <div class="body-content">
    <form method="post" class="form-x" th:action="@{/emp/addEmp}">
  
      <div class="form-group">
        <div class="label">
          <label>员工姓名：</label>
        </div>
        <div class="field">
          <input type="text" class="input" name="ename" id="ename"/>
          <div class="tips"></div>
        </div>
      </div>  
      
      <div class="form-group">
        <div class="label">
          <label>员工性别：</label>
        </div>
    
        <div class="field"  style="padding-top: 9px;">
          <input type="radio" name="esex" value="1" checked="checked"/>男;
          <input type="radio" name="esex" value="0"/>女;
          <div class="tips"></div>
        </div>
      </div>
  
      <div class="form-group">
        <div class="label">
          <label>岗位：</label>
        </div>
        <div class="field">
          <input type="text" class="input" name="egw" id="egw"/>
          <div class="tips"></div>
        </div>
      </div> 
  
      <div class="form-group">
        <div class="label">
          <label></label>
        </div>
        <div class="field">
          <button class="button bg-main icon-check-square-o" type="submit"> 提交</button>
        </div>
      </div>
    </form>
  </div>
</div>
</body>

</html>

```

1. 包含一个简单的表单，用户可以在表单中输入员工的姓名、性别和岗位信息
2. 并通过点击提交按钮将这些信息提交到 `EmpController.java.emp.addEmp`路径,这个路径将由服务器端的相应处理方法（Controller）处理，以完成员工信息的添加

`【com/hjc/springbootmovies/controller/EmpController.java】`

```
@RequestMapping(value = "addEmp" ,method = RequestMethod.POST)
    public String addEmp(ModelEmp modelEmp){
        int count = empService.addEmp(modelEmp);
        return"html/emp/all";
    }
```

1. 通过提交的表单数据创建一个 ModelEmp对象
   1. 将一个叫做 `modelEmp`的对象添加到 `empService`中
   2. 返回一个 `int`类型的值，这个值被赋给了一个叫做 `count`的变量
   3. `src/main/java/com/hjc/springbootmovies/service/EmpService.java`

      ```
      package com.hjc.springbootmovies.service;

      import com.hjc.springbootmovies.entity.ModelEmp;

      public interface EmpService {
          int addEmp(ModelEmp modelEmp);
      }
      ```
   4. `src/main/java/com/hjc/springbootmovies/service/Impl/EmpServiceImpl.java`

      ```
      package com.hjc.springbootmovies.service.Impl;

      import com.hjc.springbootmovies.entity.ModelEmp;
      import com.hjc.springbootmovies.mapper.MappingEmp;
      import com.hjc.springbootmovies.service.EmpService;

      @Service
      public class EmpServiceImpl implements EmpService {
          @Autowired
          private MappingEmp mappingEmp;

          @Override
          public int addEmp(ModelEmp modelEmp) {
              return mappingEmp.addEmp(modelEmp);
          }
      }

      ```
   5. `src/main/java/com/hjc/springbootmovies/mapper/MappingEmp.java`

      ```
      package com.hjc.springbootmovies.mapper;

      import com.hjc.springbootmovies.entity.ModelEmp;

      @Mapper
      public interface MappingEmp {

          @Insert("INSERT INTO emp(ename,esex,egw) VALUES(#{ename} ,#{esex} ,#{egw} )")
          @Options( useGeneratedKeys = true , keyColumn = "eid")
          int addEmp(ModelEmp modelEmp);

      }

      ```
   6. 
2. 然后调用 empService的 addEmp方法进行员工信息的添加
3. 返回"html/emp/all""

3.主界面

`【src/main/resources/templates/html/emp/all.html】`

1. 点击修改按钮
