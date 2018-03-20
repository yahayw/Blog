## HTML表单
### 目的/作用：收集用户信息（如注册/登录时）
### 注意：标签`<form></form>`包裹住的表单信息能成功提交，form标签外的表单信息提交无效。
### 表单标签1：
   #### `<input type="xxx" name="xxx" id="xxx">` //inline element<br/>
      1. **type属性**的值：
         <br/>
         **text**     //单行文本框。<br/>
         **passport** //密码框，输入内容显示为神秘的黑色原点。<br/>
         **checkbox** //复选框，name属性值相等为“同组”，有checked属性的复选框默认是“选中”状态。<br/>
         **radio**    //单选框，name属性值相等为“同组”，有checked属性的复选框默认是“选中”状态。<br/>
         **button**   //按钮。<br/>
         **submit**   //“提交表单”功能按钮。<br/>
         **file**     //上传文件。<br/>
         **hidden**   //对用户隐藏的“校验信息”，用于校验用户的合法性、阻止CSRF攻击。<br/>
         **email_HTML5_**  //邮箱地址框，如果邮箱地址输入错误，会给出提示。<br/>
         **number_HTML5_**  //数字输入框，限制用户只能输入数字。<br/>
      2. **name属性**的作用：<br/>
         表单提交到后台后，后台接收到的是“键值对”形式的数据-----**name:value**。 <br/>
         这个**name**就是表单标签的**name属性值**。 <br/>
         这个**value**就是用户输入的内容/表单标签的**value属性值**。 <br/>
      3. **id属性**的作用：<br/>
         表单标签的id属性往往是为了配合label标签使用，<label for="id属性值">提示输入信息:</label>。<br/>
         `for="id属性值"`确定label提示的是哪个input框。<br/>
         点击label的内容就会focus到对应的input框。<br/>
#### `select标签 `<br/>
       <select name="">
            <option value="">...</option>
            <option value="" selected>...</option>
            <option value="">...</option>
       </select>
       //下拉菜单
       //默认显示出有selected属性的子元素<br/>
#### `textarea标签`多行文本
      <textarea name="" cols="" rows="">多行文本框</textarea>
#### 提交表单功能按钮
      - <button>提交</button> 需要在form标签包裹下，否则就是普通按钮
      - <input type="submit" value="提交">
#### 表单包裹标签
     `<form action="" method="get/post">各种收集信息的表单标签</form>`
     <br/>
     **action
一个处理这个form信息的程序所在的URL。这个值可以被 <button> 或者 <input> 元素中的 formaction 属性重载（覆盖）**
   <br/>
   **method
浏览器使用这种 HTTP 方式来提交 form. 可能的值有:get（默认）和post。**
   <br/>
1. post: 指的是 HTTP POST 方法  表单数据会包含在表单体内然后发送给服务器.
2. get: 指的是 HTTP GET 方法; 表单数据会附加在 action 属性的URI中，并以 '?' 作为分隔符, 然后这样得到的 URI 再发送给服务器. 当这样做（数据暴露在URI里面）没什么副作用，或者表单仅包含ASCII字符时，再使用这种方法吧。**
   > **post提交方式因为不会把信息拼接到URL上，所以更具有保密性，且能传送较大的数据量，适合向后台提交数据。**
   > **因为get提交方式的“拼接表单数据到URL”的这一特点、URL的最大长度室友限制的，所以get方式提交的数据量小且保密性差，更适合向后台要数据**

