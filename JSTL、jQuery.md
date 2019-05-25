# 一、JSTL标签和EL表达式

## 1. JSTL简介

- JSTL（Javaserver Pages Standard Tag Liabrary）是一个JSP标准标签库，用来解决像遍历Map或集合、条件测试、XML处理，数据库访问和数据库操作等常见问题。

- JSTL由五个功能不同的标签库组成：**核心标签库**、**格式标签库**、**SQL标签库**、**XML标签库**和**函数标签库**。

- 在JSP页面中使用JSTL库，必须通过以下格式使用 `taglib` 指令：

  ```jsp
  <%@ taglib prefix="c" url="http://java.sun.com/jsp/jstl/core" %> <!--要是用核心标准库-->
  ```



## 2. 核心标签库

### 2.1 表达式标签

- 前缀"c"，在JSTL的核心标签库中，包含了`<c:out>、<c:set>、<c:remove>、<c:catch>`四个表达式标签

#### 2.1.1 out 输出标签

- `<c:out>` 标签用于在运算表达式时，将结果输出到当前的JspWriter，类似于JSP表达式`<%=expression%>`或EL表达式`${expression}`。

- `<c:out>`标签的语法格式：

  ```jsp
  <c:out value="hello world" escapeXml="" default="defaultValue">
  ```

  - value：用于指定要输出的变量或表达式，可使用EL表达式，如：`value="${expression}"`。
  - escapeXml：可选属性，用于指定是否转换特殊字符，默认值为true，表示转换。
  - default：可选属性，用于指定当value属性值为null时，将要显示的默认值。

#### 2.1.2 set 变量设置标签

- `<c:set>`标签的三个作用：

  - 创建一个字符串和一个引用该字符串的有界变量

  - 创建一个引用现存有界对象的有界变量

  - 设置有界变量的属性

    > 说明：有界变量是指在指定范围内（page、request、session、application）有效的变量

- `<c:set>`标签的语法格式：

  ```jsp
  <!--第一种：创建一个有界变量，并用value属性指定一个字符串或现存的有界对象-->
  <c:set var="varName" value="value" scope="" />
      
  <!--第二种：创建一个有界变量，并用标签体指定一个字符串或现存的有界对象-->
  <c:set var="varName" scope="">
      标签体
  </c:set>
     
  <!--第三种：设置有界对象的属性值，并通过value属性进行赋值-->
  <c:set target="target" property="propertyName" value="value"/>
  <!--例：将字符串“beijing”赋予有界对象address的city属性-->
  <c:set target="${address}" property="city" value="beijing"/>
  
  <!--第四种：设置有界对象的属性值，并通过标签体进行赋值-->
  <c:set target="target" property="propertyName">
      标签体
  </c:set>
  ```

  - var：要创建的有界变量名
  - value：用于指定一个字符串或现存的有界对象，可以使用EL
  - scope：用于指定变量的作用域，默认为page
  - target：用于指定储存变量值或标签体的目标对象，必须是JavaBean或Map集合对象
  - property：用于指定目标对象存储数据的属性名

#### 2.1.3 remove 变量移除标签

- `<c:remove>`标签用于删除有界变量

- `<c:remove>`标签的语法格式：

  ```jsp
  <c:remove var="varName" [scope="{page|request|session|application"]/>
  ```

  - var：要删除的有界变量的名称
  - scope：指定要删除的有界变量的范围。如果没有指定有界变量的范围，将分别在page、request、session和application的范围内查找要移除的变量并移除

#### 2.1.4 catch 捕获异常标签

- `<c:catch>`标签用于捕获程序中出现的异常

- `<c:catch>`标签的语法格式：

  ```jsp
  <c:catch [var="exception"]>
  	<!--可能存在异常的代码-->
  </c:catch>
  ```

  - var：可选属性，用于指定储存异常信息的变量

### 2.2 URL标签

- import
- redirect
- url
- param

### 2.3 流程控制标签

- if
- choose
- when
- otherwise

### 2.4 便利标签

- forEach
- forTokens





# 二、jQuery

## 1. jQuery 简介

- 教程链接：<http://how2j.cn/k/jquery/jquery-tutorial/467.html>

-  jQuery是一个JavaScript的框架，是对JavaScript的一种封装。通过jQuery可以非常方便的**操作HTML的元素**。

- 理解 `$(function(){});`

  - 表示文档加载，这是为了防止文档在完全加载（就绪）之前运行jQuery代码

  - 换句话说，写在这里面的jQuery代码都是文档加载好之后的

  - 另一种写法：`$(document).ready(function(){});`

  - 示例：

    ```html
    <script src="http://how2j.cn/study/jquery.min.js"></script>
     
    <script >
    $(function(){
      document.write("文档加载成功!");
      document.close();
    });
    </script>
    
    ```

- jQuery通过 `$("#id")` 获取元素

- 增加监听器：

  - 与原生JavaScript需要在html元素上增加监听事件不同的是，**jQuery不需要在html元素上进行操作**，这样的好处是，**html只需要显示内容**，特别是业务复杂起来之后维护js代码会更加容易

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              alert("点击了按钮！")；
          });
      });
  </script>
  <button id="b1">按钮</button>
  ```

- 显示与隐藏示例：

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              $("$d").hide();
          });
          $("#b2").click(function(){
              $("#d").show;
          });
      });
  </script>
  
  <button id="b1">隐藏div</button>
  <button id="b2">显示div</button>
  
  <div id="d">这是一个div</div>
  ```



## 2. jQuery 常见方法

### 2.1 取值 val()

- 通过jQuery对象的 val() 方法获取值，相当于 document.getElementById("input").value

- 示例：

  ```html
  <script>
      $(function(){
          %("#b1").click(function(){
              alert($("input1").val());
          });
      });
  </script>
  <button id="b1">取值</button>
  <input type="text" id="input1" value="默认值">
  ```

### 2.2 获取元素内容 html()

- 通过 html() 获取元素内容，如果有子元素，保留标签

- 示例：

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              alert($("#d1").html());
          });
      });
  </script>
  <button id="d1">获取文本内容</button>
  <div d="d1">
      这是div的内容
      <span>这是div里的span</span>
  </div>
  ```

### 2.3 获取元素内容 text()

- 通过 text() 获取元素内容，如果有子元素，不包含标签

- 示例：

  ```html
  <!--将上面示例的html()换成text()-->
  ```



## 3. jQuery CSS

### 3.1 增加class addClass()

- 通过 addClass() 增加一个样式中的class

- 示例：

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              $("#d").addClass("pink");
          });
      });
  </script>
  <button id="b1">增加背景色</button>
  <style>
      .pink{
          background-color:pink;
      }
  </style>
  
  <div id="d">
      Hello jQuery
  </div>
  ```



### 3.2 删除class removeClass()

- 通过removeClass() 删除一个样式中的class

- 示例：

  ```html
  <!--将上面示例中的addClass()换成removeClass()-->
  ```



### 3.3 切换class toggleClass()

- 通过 toggleClass() 切换一个样式中的class

- 这里的切换指的是：如果存在就删除；如果不存在就添加

- 示例：

  ```html
  <!--将上面示例中的addClass()换成toggleClass()-->
  ```



### 3.4 CSS函数

- 通过CSS函数，直接设置样式：

  - css(property, value)
  - css({p1:v1, p2:v2})

- 示例：

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              $("#d1").css("background-coler","pink");
          });
          $("#b2").click(function(){
              $("#d2").css({"background-cplor":"pink", "color":"green"});
          });
      });
  </script>
  <button id="b1">设置单一样式</button>
  <button id="b2">设置多种样式</button>
  
  <div id="d1">
      单一样式，只设置背景颜色
  </div>
  <div id="d2">
      多种样式，设置背景颜色和字体颜色
  </div>
  ```



## 4. jQuery 选择器

### 4.1 元素

- `<div> </div>`

- `$("tagName")` 根据标签名，选择所有该标签的元素 

- 示例：

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              $("div").addClass("pink"); //给所有的div元素增加粉色背景
          });
      });
  </script>
  ```



### 4.2 id

- `<button id="b"></button>`
- `$("#id")` 根据 id 选择元素，id 应该是唯一的，如果 id 重复，则只会选择第一个。



### 4.2 类

- `<div class="c"></div>`

- `$(".className")` 根据 class 选择元素

- 示例：

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              $(".c").addClass("pink");
          });
      });
  </script>
  <button id="b1">给class="c"的div增加背景色</button>
  
  <style>
      .pink{
          background-color:pink;
      }
  </style>
  <div class="c">
      Hello jQuery
  </div>
  ```



### 4.3 层级

- `$("selector1 selector2")` 选择selector1下的selector2元素

- 示例：

  ```html
  <script>
  	$(function(){
          $("#b1").click(fuinction(){
          	$("div#d3 span").addClass("pink");               
          });
      });
  </script>
  <style>
      .pink{
          background-color:pink;
      }
  </style>
  <div id="d3">
      <span>Hello JQuery</span>
  </div>
  ```



### 4.4 最先最后

- `$(selector:first)` 满足选择器条件的第一个元素

- `$(selector:last)` 满足选择器条件的最后一个元素

- 示例：

  ```html
  <script>
  	$(function(){
          $("#b1").click(function(){
              $("div:first").addClass("pink");
          });
          $("#b2").click(function(){
              $("div:last").addClass("pink");
          });    
      });
  </script>
  ```



### 4.5 奇偶

- `$(selector:odd)` 选择满足条件的奇数元素

- `$(selector:even)` 选择满足条件的偶数元素

  > 注：因为是**基零**的，所以第一排的下标其实是0（偶数）

- 示例：

  ```html
  <script>
  	$(function(){
          $("#b1").click(function(){
              $("div:odd").toggleClass("pink");
          });
          $("#d2").click(function(){
              $("div:even").toggleClass("pink");
          });
      });
  </script>
  ```



### 4.6 可见性

- `$(selector:hidden)` 满足选择器条件的不可见的元素

- `$(selector:visible)` 满足选择器条件的可见的元素

  > 注：div:visible 和 div:visible（空格）是不同的意思，前者表示选中可见的div；后者表示选中div下可见的元素



### 4.7 属性

- `$(selector[attribute])` 满足选择器条件的**有某属性的**元素：

- `$(selector[attribute=value])` 满足选择器条件的属性**等于value**的元素

- `$(selector[attribute^=value])` 满足选择器条件的属性**以value开头**的元素

- `$(selector[attribute$=value])` 满足选择器条件的属性**以value结尾**的元素

- `$(selector[attribute*=value])` 满足选择器条件的属性**包含value**的元素

- 示例：

  ```html
  <script>
  	$(function(){
          $("#b1").click(function(){
              $("div[id]").toggleClass(border);
          });
          $("#b2").click(function(){
        		$("div[id='pink']").toggleClass("border");
     		});
    		$("#b3").click(function(){
        		$("div[id!='pink']").toggleClass("border");
     		});
     		$("#b4").click(function(){
        		$("div[id^='p']").toggleClass("border");
     		});
     		$("#b5").click(function(){
        		$("div[id$='k']").toggleClass("border");
     		});
     		$("#b6").click(function(){
        		$("div[id*='ee']").toggleClass("border");
     		});
      });
  </script>
  ```



### 4.8 表单对象

- 表单对象选择器指的是选中form下会出现的输入元素

- **:input** 会选择所有的输入元素，不仅仅是input标签开始的那些，还包括textarea、select和button

- **:button** 会选择type=button的input元素和button元素

- **:radio** 会选择单选框

- **:checkbox** 会选择复选框

- **:text** 会选择文本框，但是不会选择文本域

- **:submit** 会选择提交按钮

- **:image** 会选择图片型提交按钮

- **:reset** 会选择重置按钮

- 示例：

  ```html
  <script>
  	$(function(){
          $(".b").click(function(){ //点击class为b的button
              var value = $(this).val(); // 获取此button的值value
              $("td[rowspan!=13] "+value).toggle(500); // 属性+层级定位元素
          });
      });
  </script>
  ```



## 5. jQuery 筛选器

### 5.1 第一个 最后一个 第几个

- 首先通过`$("div")` 选择多个div元素，接下来做进一步的筛选

- **first()** 第一个元素

- **last()** 最后一个元素

- **eq(num)** 第num个元素

  > 注：num 基是0

- 示例：

  ```html
  <script>
  	$(function(){
          $("#b1").click(function(){
              $("div").first().toggleClass("pink");
          });
          $("#b2").click(function(){
              $("div").last().toggleClass("pink");
          });
          $("#b3").click(function(){
              $("div").eq(4).toggleClass("pink");
          });
      });
  </script>
  ```



### 5.2 父 祖先

- **parent()** 选取最近的一个父元素

- **parents()** 选取所有的祖先元素

- 示例：

  ```html
  <script>
      $(function(){
          $("#b1").click(function(){
              $("#currentDiv").parent.toggleClass("b");
          });
          $("#b2").click(function(){
              $("#currentDiv").parents.toggleClass("b");
          });
      });
  </script>
  ```



### 5.3 儿子 后代

- **children()** 筛选出儿子元素（紧挨着的子元素）

- **find(selector)** 筛选出后代元素

- 示例：

  ```html
  <script>
  $(function(){
    $("#b1").click(function(){
       $("#currentDiv").children().toggleClass("b");
    });
    $("#b2").click(function(){
       $("#currentDiv").find("div").toggleClass("b");
    });
     
  });
  </script>
  ```



### 5.4 同级

- sibling() 同级元素

- 示例：

  ```html
  <script>
  $(function(){
    $("#b1").click(function(){
       $("#currentDiv").siblings().toggleClass("b");
    });
  });
  </script>
  ```



## 6. jQuery 属性

### 6.1 获取

- attr() 获取一个元素的属性

- 示例：

  ```html
  <script>
  $(function(){
      $("#b1").click(function(){
          alert("align属性是：" + $("#h").attr("align"));
      });
      $("#b2").click(function(){
          alert("game属性是：" + $("#h").attr("game"));
      });
  }));
  </script>
  <button id="b1">获取align属性</button>
  <button id="b2">获取自定义game属性</button>
  
  <h1 id="h" align="center" game="LOL">居中标题</h1>
  ```



### 6.2 修改

- attr(attr, value) 修改属性

- 示例：

  ```html
  <script>
  $(function(){
      $("#b1").click(function(){
          $("#h").attr("align", "right");
      });
  });
  </script>
  <button id="b1">修改align的属性为right</button>
  <h1 id="h" align="center">居中标题</h1>
  ```



### 6.3 删除

- removeAttr(attr) 删除属性

- 示例：

  ```html
  <script>
  $(function(){
     $("#b1").click(function(){
           $("#h").removeAttr("align");
     });
  });   
  </script> 
  <button id="b1">删除align属性</button> 
  <h1 id="h" align="center" game="LOL">居中标题</h1>
  ```



### 6.4 prop和attr的区别

- 与 **prop** 一样 **attr** 也可以用来获取和设置元素的属性

- 区别在于，对于自定义属性和选中属性的处理，选中属性指的是checked、selected这两种属性：

  1. 对于自定义属性，attr能够获取，prop不能获取
  2. 对于选中属性：
     - attr 只能获取初始值，无论是否变化
     - prop能够访问变化后的值，并且以true|false的布尔型返回

- 所以在访问表单对象属性的时候，应该采用prop而非attr

- 示例：

  ```html
  <script>
  $(function(){
      $("#b1").click(function(){
          alert("game属性是：" + $("#c").attr("game")); // LOL
      });
      $("#b2").click(function(){
          alert("game属性石：" + $("#c").prop("game")); // undefined
      });
      $("#b3").click(function(){
          alert("checked属性是：" + $("#c").attr("checked")); // checked
      });
      $("#b4").click(function(){
         alert("checked属性是：" + $("#c").prop("checked"));//true|false
      });
  });
  </script>
  <input type="checkbox" id="c" game="LOL" checked="checked">
  ```

  

## 7. jQuery 效果

- （暂时跳过）



## 8. jQuery 事件

### 8.1 加载

- 页面加载有两种方式：

  1. `$(document).ready();`
  2. `$();` （较常用）

- 图片加载用 `load()` 函数

- 示例：

  ```html
  <script>
  $(document).ready(function(){
      $("#message1").html("页面加载成功");
  });
  $(function(){
      $("#img").load(function(){
         $("#message2").html("图片加载成功"); 
      });
  });
  </script>
  <div id="message1"> </div>
  <div id="message2"> </div>
  <img id="img" src="http://how2j.cn/example.gif">
  ```



### 8.2 点击

- click() 表示单击

- dblclick() 表示双击

  > 注：空白键和回车也可以造成click事件，但是只有**双击鼠标**才能造成dblclick事件

- 示例：

  ```html
  <script>
  	$(function(){
          $("#b").click(function(){
              $("#message").html("单击按钮");
          });
          $("#b").dblclick(function(){
              $("#message").html("双击按钮");
          });
      });
  </script>
  <div id="message"></div>
  <button id="b">测试单击和双击</button>
  ```



### 8.3 键盘

- keydown 表示按下键盘
- keypress 表示按住键盘
- keyup 表示键盘弹起
- 先后顺序：keydown、keypress、keyup



### 8.4 鼠标

- mousedown 表示鼠标按下
- mouseup 表示鼠标弹起
- mousemove、mouseenter、mouseover表示鼠标进入
  - mousemove：当鼠标进入元素，**每移动一下** 都会被调用
  - mouseenter：当鼠标进入元素，调用以下，**在其中移动，不调用**；当鼠标经过其子元素不会被调用
  - mouseover：当鼠标进入元素，调用一下，**在其中移动，不调用**；当鼠标经过其子元素会被调用
- mouseleave、mouseout表示鼠标离开
  - mouseleave：当鼠标经过其子元素不会被调用
  - mouseout：当鼠标经过其子元素会被调用



### 8.5 焦点

- focus() 获取焦点

- blur() 失去焦点

- 示例：

  ```Html
  <script>
  	$(function(){
      	$("input").focus(function(){
      		$(this).val("获取了焦点");
      	});
          $("input").blur(function(){
              $(this).val("失去了焦点");
          });
      });
  </script>
  <input type="text">
  <input type="text">
  ```



### 8.6 改变

- change() 内容改变

  > 注：对于文本框，只有当该文本失去焦点的时候，才会触发change事件

- 示例：

  ```html
  <script>
  	$(function(){
          $("#input").change(function(){
              var text = $(text).val();
              $("#message").html("input1的内容变为了："+text);
          });
      });
  </script>
  <div id="message" type="text"></div>
  <input size="50" id="input2"type="text" value="只有当input1失去焦点的时候，才会触发change事件" >
  ```



## 8.7 提交

- submit() 提交form表单

- 示例：

  ```html
  <script>
  	$(function(){
          $("#form").submit(function(){
              alert("提交账号密码");
          });
      });
  </script>
  <form id="form" action="">
      账号：<input name="name" type=""><br>
      密码：<input name="password" type=""><br>
      <input type="submit" value="登录">
  </form>
  ```



### 8.8 绑定事件

- `$("selector").on("event",function)` 以上所有事件，都可以通过 on() 绑定事件来处理

- 示例：

  ```html
  <script>
  	$(function(){
          $("#b").on("click",function(){
              $("#message").html("单击按钮");
          });
          $("#b").on("click",function(){
              $("#message").html("双击按钮");
          });
      });
  </script>
  <div id="message"></div>
  <button id="b">测试单击和双击</button>
  ```



### 8.9 触发事件

- `$("selector").triggle("event");` 触发事件，在本例中，文档加载好之后，就触发dblclick双击事件，而不是通过去手动双击

- 示例：

  ```html
  <script>
    $(function(){
        $("#b").on("click",function(){
            $("#message").html("单击按钮");
        });
        $("#b").on("dblclick",function(){
            $("#message").html("双击按钮");
        });
       $("#b").trigger("dblclick");
    });
  </script>
      
  <div id="message"></div>
    
  <button id="b">测试单击和双击</button>
  ```



## 9. jQuery AJAX

### 9.1 提交AJAX请求

- 格式：

  ```html
  $.ajax({
  	url:page,
  	data:{"name":value},
  	success:function(result){
  		$("#checkResult").html(result);
  	}
  });
  ```

- $.ajax采用参数集的方式{param1,param2,param3}，不同的参数之间用逗号隔开

  - 第一个参数 **url:page** 表示访问的是page页面
  - 第二个参数 **data:{name:value}** 表示提交的参数
  - 第三个参数 **success:function(){}** 表示服务器成功返回后对应的响应函数

- 示例：

  ```html
  <div id="checkResult"></div>
  输入账号：<input id="name" type="text">
  <script>
  	$(function(){
          $("#name").keyup(function(){
              var page="/study/checkName.jsp";
              var value = $(this).val();
              $.ajax({
                  url:page,
                  data:{"name":value},
                  success:function(result){
                      $("#checkResult").html(result);
                  }
              });
          });
      });
  </script>
  ```



### 9.2 使用get方式提交ajax

- **$.get** 是 **$.ajax** 的简化版，专门用于发送GET请求

- 格式：

  ```html
  $.get(
  	page,
  	{"name":value},
  	function(result){
  		$("#checkResult").html(result);
  	}
  );
  ```

- 只有第一个参数是必须的，其他都是可选的

- 示例：

  ```html
  <div id="checkResult"></div>
  输入账号：<input id="name" type="text">
  <script>
  	$(function(){
          $("#name").keyup(function(){
              var page = "/stydy/checkName.jsp";
              var value = $(this).val();
              $.get(
                  page,
                  {"name":value},
                  function(result){
                      $("#checkResult").html(result);
                  }
              );
          });
      });
  </script>
  ```



### 9.3 使用post方式提交ajax

- **$.post** 是 **$.ajax** 的简化版，专门用于发送POST请求

- 格式：

  ```html
  $.post(
  	page,
  	{"name":value},
  	function(result){
  		$("#checkResult").html(result);
  	}
  );
  ```

- get 和 post 的区别：

  - **get：**
    - 是form默认的提交方式
    - 如果通过一个超链访问某个地址，是get方式
    - 如果在地址栏直接输入某个地址，是get方式
    - 提交数据会在浏览器显示出来
    - **不可以**用于提交二进制数据，比如上传文件
  - **post：**
    - 必须在form上通过method="post" 显示指定
    - 提交数据不会再浏览器显示出来
    - **可以**用于提交二进制数据，比如上传文件



### 9.4 最简单的调用ajax的方式 load()

- **load()** 比起 **$.get** 和 **$.post** 就更简单

- `$("#id").load(page, [data]);`

  - id： 用于显示ajax服务端文本的元素id
  - page： 服务端页面
  - data： 提交的数据，可选。在本例中，直接在page里加上了参数列表

- 示例：

  ```html
  <div id="checkResult"></div>
  输入账号：<input id="name" type="text">
  <script>
  	$(function(){
          $("#name").keyup(function(){
              var value=$(this).val();
              var page = "/study/checkName.jsp?name="+value;
              $("#checkResult").load(page);
          });
      });
  </script>
  ```



### 9.5 格式化form下的输入数据

- serialize()： 格式化form下的输入数据

- 有时候form下的输入内容比较多，一个一个的取比较麻烦，就可以使用serialize() 把输入数据格式化成字符串

- 示例：

  ```html
  <div id="checkResult"></div>
  <div id="data"></div>
  <a herf="http://how2j.cn/study/checkName.jsp">http://how2j.cn/study/checkName.jsp</a>
  
  <form id="form">
  输入账号：<input id="name" type="text" name="name"><br>
  输入年龄：<input id="age" type="text" name="age"><br>
  手机号码：<input id="mobile" type="text" name="mobile"><br>
  </form>
  
  <script>
  $(function(){
      $("input").keyup(function(){
          var data=$("#form").serialize();
          var url="http://how2j.cn/study/checkName.jsp";
          var link = url+"?"+data;
          $("a").html(link);
          $("a").attr("herf",link);
      });
  });
  </script>
  ```

  

## 10. jQuery 数组操作

### 10.1 遍历

- `$.each(a, function(i, n){})` 遍历一个数组

  - 第一个参数是数组
  - 第二个参数是回调函数，i是下标，n是内容

- 示例：

  ```html
  <script>
  	var a = new Array(1,2,3);
  	$.each(a, function(i, n){
          document.write("元素[" + i "] : " + n + "<br>");
      })
      document.close();
  </script>
  
  //结果
  元素[0] : 1
  元素[1] : 2
  元素[2] : 3
  ```

  

### 10.2 去除重复

- `$.unique()` 去掉重复的元素

  > 注意：执行unique之前，要先调用sort对数组的内容进行排序

- 示例：

  ```html
  <script>
  	var a=new Array(5,2,4,2,3,3,1,4,2,5);
      a.sort();
      $.unique(a);
      $.each(a, function(){
          document.write("元素[" + i + "] : " + n + "<br>");
      })
      document.close();
  </script>
  
  //结果
  元素[0] : 1
  元素[1] : 2
  元素[2] : 3
  元素[3] : 4
  元素[4] : 5
  ```



### 10.3 是否存在

- `$.inArray` 返回元素在数组中的位置，如果不存在返回-1

- 示例：

  ```html
  <script>
  	var a=new Array(1,2,3,4,5,6);
      document.write($.inArray(9,a));
      document.close();
  </script>
  
  //结果
  -1
  ```

  

## 11. jQuery 字符串操作

### 11.1 去除首尾空白

- `$.trim()` 去除首尾空白

- 示例：

  ```html
  <script>
  	document.write($.trim(" hello jquery   "));
      document.close();
  </script>
  ```

  

## 12. jQuery JSON

### 12.1 将JSON格式的字符串，转换为JSON对象

- `$.parseJSON()` 将JSON格式的字符串，转换为JSON对象

- 示例：

  ```html
  <script>
  	var s1 = "{\"name\":\"盖伦\"";
      var s2 = ",\"hp\":616}";
      var s3 = s1 + s2;
      
      document.write("这是一个JSON格式的字符串：" + s3);
      document.write("<br>");
      var gareen  = $.parseJSON(s3);
      
      document.write("这是一个JSON对象：" + gareen);
  </script>
  
  // 结果
  这是一个JSON格式的字符串:{"name":"盖伦","hp":616}
  这是一个JSON对象: [object Object]
  ```

  

## 13. jQuery 对象转换