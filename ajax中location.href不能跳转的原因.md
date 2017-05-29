# $.ajax window.location.href 问题
#### 在工作中遇到通过$.ajax异步请求后处理返回页面，然后直接跳转到另一个页面，使用window.location.href,请求始终不能执行，问题是async为false 时，即异步，window.location.href失效。解决方法是:

``` javascript
 <script type="text/javascript">
 $("#myForm").submit(function(){
    $.ajax({
        cache: true,
        type: "POST",
        url: "/BasketBall/user/validate",
        data:$('#myForm').serialize(),// 你的formid
        async: false,
        error: function(request) {  
            alert("Connection error");
        },
        success: function(data) {
            if(data == "false"){
                window.location.href="/BasketBall/index2.html";
            }else if (data == "true"){
                alert("账号或密码错误")
            }
        }
    });
    //一般情况下要加上：return false
    return false;
}

```
