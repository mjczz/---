## success和error方法会自动判断当前请求是否属于Ajax请求，如果属于Ajax请求则会调用ajaxReturn方法返回信息。 ajax方式下面，success和error方法会封装下面的数据返回：
### 1.$data['info']   =   $message; // 提示信息内容
### 2.$data['status'] =   $status;  // 状态 如果是success是1 error 是0
### 3.$data['url']    =   $jumpUrl; // 成功或者错误的跳转地址

### 列：
```javascript
    function del(id) {
          $.get("__CONTROLLER__/del?id=" + id, function (data) {
              if (confirm("确定删除吗?")) {
                  if (data.info == 1) {
                      $("tr[alt='" + id + "']").fadeOut(500);
                      //页面跳转
                      location.href = data.url;
                  } else {
                      alert("删除失败");
                  }
              }
          }, "json");
      }
 ```
 ## 后台代码：
 #### //删除用户组用户
 ``` javascript
     public function del() {
        $id = $_GET('id');
        $model = M('group');
        if ($model->delete($id)) {
            //1给前台data.info,U给前台data.url
            $this->success(1, U('Admin/index'));
        } else {
            $this->error('删除失败');
        }
    }
```
