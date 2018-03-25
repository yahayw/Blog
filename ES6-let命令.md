

### ECMAScript的简单历史介绍：
JavaScript由Netscape公司创造，网景公司在1996年将JavaScript提交给ECMA(一个标准化组织)，提交的目的是“希望JavaScript语言能够有国际标准”。
1997年，ECMA组织发布ECMA-262标准文件的第一版（ECMAScript第一版/ECMAScript1.0/ES1.0）。
后来这一标准文件ECMA-262 / ECMAScript 继续增删修改，发布更新的标准版本。
在ECMA-262第6版 / ecmascript6 /ES6 出现以前，JS学习者主要学习ES3和ES5（ES4在制定成员的分歧下，最终被废），最初构想的ES4的新增内容一部分出现在ES6中。
ES6最新发布于2015年，2015年的ES6也叫ES2015，后来在每年6月发布了ES2016和ES2017，都是ES6，只是每次做了一些内容调整，因此，ES6包括了ES2015、ES2016、
ES2017。

**ECMAScript是JavaScript的规格、标准，JavaScript是ECMAScript的一种具体实现。**


### ES6的部分新内容：
下面有：**let** ****

## let命令
let的效果：
1. 产生块作用域，即，用let命令声明的变量（它）只在块内有效。
在ES6之前，JS之中只有全局作用域和函数作用域，不存在块级作用域。
    ```
    //ES6以前
    for(var i=0;i<length;i++){
    }
    console.log(i);  //10
    ```
    
    ```
    //ES6
    for(let i=0;i<10;i++){			
		}
		console.log(i) //报错：Uncaught ReferenceError: i is not defined，因为let生成了块级作用域
    ```
缺少块级作用域的坏影响有：内层同名变量会覆盖外层同名变量，如下代码
    ```
    var tmp = new Date();
    function f() {
      console.log(tmp);
      if (false) {
        var tmp = 'hello world';
      }
    }
    f(); // undefined
    ```



2. 使变量不声明前置：
   尽量养成先声明变量后使用变量的习惯
   ```
   //ES6以前
   console.log(a); //undefined
   var a = 1;//用var声明的变量a发生了"声明前置"
   ```
   
   ```
   //ES6
   console.log(b); //报错
   let b = 2; //用let声明的变量不会有“声明前置”
   ```
   
3. 暂时性死区   
假设一个块内部有let命令声明的变量，块外有同名变量，那么在块内的lei声明变量的前面使用同名变量，会被视作为lei声明的变量----在let声明前使用会报错。
来看一看这句话的代码表述：
    ```
        var num = 3;
	if(true){
		console.log(num); //报错：Uncaught ReferenceError: num is not defined
		let num = "num";
	}
    ```
块里无let声明和块外同名的变量：
    ```
        let num =3;
	if(true){
		console.log(num) //3
		let b = 4;
	}
    ```
    
4. 不允许同一块作用域下重复声明同一变量
    ```
        if(true){
		let a = 1;
		var a = 2; //报错
	}
    ```
    
    ```
        function func() {
		  let a = 1;
		  let a = 2;
	}
	func() //报错
    ```
    
    ```
	for(let i=0; i<10; i++){ //i在()的块级作用域中
		let i="string"; //不报错 i在{}块级作用域中
		// let i = true; //报错，i在{}块级作用域中
		if(true){
			let i=100;//不报错，i在{}的{}块级作用域中
		}
	}
    ```
   


