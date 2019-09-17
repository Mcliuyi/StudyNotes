## 使用Gson从前端发送对象列表，后台使用Gson进行格式转换



1. 前端发送数据必须为对象列表形式，同时要将对象列表转换为`json`格式,，需要使用`JSON.stringify()`方法

   ```js
    var obj = {};
           obj.id="1";
           obj.num="200";
           var array = [];
           array.push(obj);
           var obj2 = {};
           obj2.id = "2";
           obj2.num = "120";
           array.push(obj2);
           $.ajax({
               type: "post",
               url: "demo",
               tiemout: 3000,
               data: {
                   "cids": JSON.stringify(array)
               },
               success: function (data) {
                   alert(data)
               },
               error: function () {
                   alert("请求出错");
               }
           })
   
   ```


2. 后台接收数据并进行转换

   ```java
   Gson gson = new Gson();
   
   //接受数据
   String data = request.getParameter("cids");
   //BeanObject 为一个javabean对象，需要和前端传过来的数据对应属性一样
   ArrayList<BeanObject>  beanObjectArrayList;
   
   Type type = new TypeToken<ArrayList<BeanObject>>() {
   }.getType();
   
   beanObjectArrayList = gson.fromJson(data, type);
   ```
