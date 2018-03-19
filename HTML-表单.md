## HTML表单
### 目的/作用：收集用户信息（如注册/登录时）
### 注意：标签`<form></form>`包裹住的表单信息能成功提交，form标签外的表单信息提交无效。
### 表单标签：
   - `<input type="xxx" name="xxx" id="xxx">` //inline element<br/>
      1. type属性的值：
      2. name属性的作用：
         表单提交到后台后，后台接收到的是“键值对”形式的数据-----name:value。<br/>
         这个name就是表单标签的name属性值。<br/>
         这个value就是用户输入的内容/表单标签的value属性值。<br/>
      3. id属性的作用：
         表单标签的id属性往往是为了配合label标签使用，<label for="id属性值">提示输入信息:</label>。
         `for="id属性值"`确定label提示的是哪个input框。
         点击label的内容就会focus到对应的input框。
        举例：<br/>
            `<label for="name">请输入姓名：</label>`
            `<input type="text" id="name">`
            `<!--点击label标签，id属性值和 label标签的for属性值 相等的input标签就会处于focus状态，可以在里面输入内容-->`
            
