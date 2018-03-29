### 简单介绍：BFC是"Block Format Context"的首字母缩写，意为块级格式化上下文。

BFC有一些特性，这些特性可以用来解决实际问题，详细介绍往下看。



### BFC的特性和作用：

1. 解决父子元素间的垂直外边距合并问题。

   需要注意：设置了border或者padding的父元素是不会出现垂直外边距合并的问题的。（因为父子元素之间有了“阻隔”）

   ```
   //父子元素垂直外边距合并
   <!--HTML-->
   	<div class="wrap">
   		<div class="ct">
   			<div class="child">
   			</div>
   		</div>
   	</div>
   /*CSS*/
   	    .wrap {
   	    	border: 1px dashed red;
   	    	background: pink;
   	    }
   		.ct	{
   			background: blue;
   		}
   		.child {
   			background: red;
   			margin-top: 20px;
   		}
   ```

   ![父子外边距合并为20px](https://github.com/yahayw/Blog/blob/master/blog-imgs/%E7%88%B6%E5%AD%90%E5%A4%96%E8%BE%B9%E8%B7%9D%E5%90%88%E5%B9%B60.PNG)

   **从这个例子得到：父子的垂直外边距如果只有一个，那么这个垂直外边距会加在父元素上**

   观察上图，蓝色部分是`<div class="ct"></div>`元素，红色部分是`<div class="child"></div>`元素，.child元素设置了`margin-top:20px;`，但是为什么出来的结果是.ct元素有了20px的margin-top？//该怎么做才能让样式加载该加的元素上呢？

   如果我给.ct元素也设置margin-top会怎么样呢？

   ```
   //父子元素垂直外边距合并
   <!--HTML-->
   	<div class="wrap">
   		<div class="ct">
   			<div class="child">
   			</div>
   		</div>
   	</div>
   /*CSS*/
   	    .wrap {
   	    	border: 1px dashed red;
   	    	background: pink;
   	    }
   		.ct	{
   			background: blue;
   			margin-top: 20px;
   		}
   		.child {
   			background: red;
   			margin-top: 20px;
   		}
   ```

   结果如图

   ![父子外边距合并为20px](https://github.com/yahayw/Blog/blob/master/blog-imgs/%E7%88%B6%E5%AD%90%E5%A4%96%E8%BE%B9%E8%B7%9D%E5%90%88%E5%B9%B60.PNG)

   得到的结果和.ct元素没有加margin-top:20px时是一样的。

   **从这个例子得到：父子的垂直外边距都设置了且值相等，垂直外边距会只加在父元素上 且 不是叠加值**

   继续探索，如果父子元素都设置了margin-top，且值大小不等，那么会发生什么呢？

   ```
   //父子元素垂直外边距合并
   <!--HTML-->
   	<div class="wrap">
   		<div class="ct">
   			<div class="child">
   			</div>
   		</div>
   	</div>
   /*CSS*/
   	    .wrap {
   	    	border: 1px dashed red;
   	    	background: pink;
   	    }
   		.ct	{
   			background: blue;
   			margin-top: 10px;
   		}
   		.child {
   			background: red;
   			margin-top: 20px;
   		}
   ```

   将父元素的margin-top设置为10px，子元素的margin-top设置为20px，得到的结果如下图：

   ![父子垂直外边距合并为20px](https://github.com/yahayw/Blog/blob/master/blog-imgs/%E7%88%B6%E5%AD%90%E5%A4%96%E8%BE%B9%E8%B7%9D%E5%90%88%E5%B9%B60.PNG)

   父子都设置了垂直外边距，但是结果是垂直外边距只加在了父元素上，值大小不等于父元素设置的10px，而是等于子元素设置的20px，为什么？

   **猜想：因为20px比10px大？**

   验证：下面把父子元素设置的垂直外边距的值交换一下

   ```
   //父子元素垂直外边距合并
   <!--HTML-->
   	<div class="wrap">
   		<div class="ct">
   			<div class="child">
   			</div>
   		</div>
   	</div>
   /*CSS*/
   	    .wrap {
   	    	border: 1px dashed red;
   	    	background: pink;
   	    }
   		.ct	{
   			background: blue;
   			margin-top: 20px;
   		}
   		.child {
   			background: red;
   			margin-top: 10px;
   		}
   ```

   得到的结果如下图：

   ![父子元素垂直外边距合并为20px](https://github.com/yahayw/Blog/blob/master/blog-imgs/%E7%88%B6%E5%AD%90%E5%A4%96%E8%BE%B9%E8%B7%9D%E5%90%88%E5%B9%B60.PNG)

   **猜想得到验证，的确当父子元素都设置了垂直外边距时，结果会只把垂直外边距加在父元素上，且会选择那个更大的垂直外边距值。**

   但是我还有一个问题：.wrap元素也是.ct元素的父元素啊，为什么它们没有发生垂直外边距合并？

   观察一下代码，**我猜想：是因为.wrap元素设置了border？ **

   下面来验证**把.wrap元素不设置border，看看结果如何**

   ```
   <!--HTML-->
   	<div class="wrap">
   		<div class="ct">
   			<div class="child">
   			</div>
   		</div>
   	</div>
   /*CSS*/
            body {
   		    border: 1px dotted;
   	    }
   	    .wrap {
   	    	/*border: 1px dashed red;*/
   	    	background: pink;
   	    }
   		.ct	{
   			background: blue;
   			margin-top: 20px;
   		}
   		.child {
   			background: red;
   			margin-top: 10px;
   		}
   ```

   ![如图](https://github.com/yahayw/Blog/blob/master/blog-imgs/%E7%88%B6%E5%AD%90%E5%A4%96%E8%BE%B9%E8%B7%9D%E5%90%88%E5%B9%B61.PNG)

   .wrap元素没有了border，也会垂直外边距合并，垂直外边距加到.wrap元素上，可见**父元素加border可以阻止父子元素外边距合并**。（父元素加padding也可以做到阻止父子元素垂直外边距合并）

   **接下来我们来验证BFC解决父子垂直外边距问题： **

   ```
   //父子元素垂直外边距合并
   <!--HTML-->
   	<div class="wrap">
   		<div class="ct">
   			<div class="child">
   			</div>
   		</div>
   	</div>
   /*CSS*/
   	    .wrap {
   	    	border: 1px dashed red;
   	    	background: pink;
   	    }
   		.ct	{
   			background: blue;
   			margin-top: 10px;
   			overflow: hidden;
   		}
   		.child {
   			background: red;
   			margin-top: 20px;
   		}
   ```

   结果如图：

   ![BFC使父子垂直外边距不再合并](https://github.com/yahayw/Blog/blob/master/blog-imgs/BFC%E8%A7%A3%E5%86%B3%E7%88%B6%E5%AD%90%E5%A4%96%E8%BE%B9%E8%B7%9D%E5%90%88%E5%B9%B6.PNG)

   ​

   ​

   ​

   ​

2. 解决父容器“感受不到”浮动子元素的存在而造成的父元素高度塌陷问题。

   父元素内部如果有浮动元素，因为浮动元素脱离普通文档流，所以默认父元素是不知道自己的里面还有浮动元素的，带来的影响如下图：**父容器高度塌陷**

   ```
   //父元素默认感受不到自己里面的浮动元素
   <!--HTML-->
   		<div class="ct">
   			父容器
   			<div class="child">
   				浮动元素
   			</div>
   		</div>
   /*CSS*/	
   		.ct {
   			width: 300px;
   			border: 2px dotted pink;
   		}
   		.child {
   			width: 100px;
   			height: 100px;
   			float: left;
   		}
   ```

   ![父容器感受不到浮动元素](https://github.com/yahayw/Blog/blob/master/blog-imgs/%E7%88%B6%E5%AE%B9%E5%99%A8%E6%84%9F%E5%8F%97%E4%B8%8D%E5%88%B0%E6%B5%AE%E5%8A%A8%E5%85%83%E7%B4%A0.PNG)

   BFC说它能解决“爸爸不认识孩子”的问题，我们来验证：

   ```
   <!--HTML-->
   		<div class="ct">
   			父容器
   			<div class="child">
   				浮动元素
   			</div>
   		</div>
   /*CSS*/	
   		.ct {
   			width: 300px;
   			border: 2px dotted pink;
   			overflow: hidden; /*.ct元素生成BFC*/
   		}
   		.child {
   			width: 100px;
   			height: 100px;
   			float: left;
   		}
   ```

   效果如图所示：

   ![BFC解决父容器高度塌陷问题](https://github.com/yahayw/Blog/blob/master/blog-imgs/BFC%E8%A7%A3%E5%86%B3%E7%88%B6%E5%AE%B9%E5%99%A8%E9%AB%98%E5%BA%A6%E5%A1%8C%E9%99%B7%E9%97%AE%E9%A2%98.PNG)

   **BFC成功解决了身为浮动元素的父容器元素的高度塌陷问题**

   ​

3. 解决浮动元素会被 文档普通流元素的文本行框包裹的问题，使普通元素“感知不到”浮动元素的存在。

   ```
   <!--HTML-->	
   	<div class="ct">
   		<div class="child">
   				浮动元素
   		</div>
   		<p>段落内容段落内容段落内容段落内容</p>
   	</div>
   /*CSS*/	
            .child {
   			width: 100px;
   			height: 30px;
   			float: left;
   			background: #FDA720;
   		}
   		p {
   			background: #ED1D7F;
   		}  
   ```

结果如下图所示：

![浮动元素被行框围绕](https://github.com/yahayw/Blog/blob/master/blog-imgs/%E6%B5%AE%E5%8A%A8%E5%85%83%E7%B4%A0%E8%A2%AB%E8%A1%8C%E6%A1%86%E5%9B%B4%E7%BB%95.PNG)

结果显示：**普通文档流元素的布局是不受浮动元素影响的，但是普通文档流元素中耳朵文本内容却默认能“看见”浮动元素，文本知道浮动元素在那就腾出空间给浮动元素。**

为了解决**行框围绕文本**的问题，我给普通元素设置生成BFC

```
<!--HTML-->	
	<div class="ct">
		<div class="child">
				浮动元素
		</div>
		<p>段落内容段落内容段落内容段落内容</p>
	</div>
/*CSS*/	
         .child {
			width: 100px;
			height: 30px;
			float: left;
			background: #FDA720;
		}
		p {
			background: #ED1D7F;
			overflow: auto;
		}  
```

结果如下图：

![BFC解决行框围绕浮动元素的问题](https://github.com/yahayw/Blog/blob/master/blog-imgs/BFC%E8%A7%A3%E5%86%B3%E8%A1%8C%E6%A1%86%E5%9B%B4%E7%BB%95%E6%B5%AE%E5%8A%A8%E5%85%83%E7%B4%A0.PNG)

生成了BFC的普通元素能看得见浮动元素。



### BFC的生成方法：

- 4类

  1. display，比如

     ```
     display: inline-block;
     display: table-cell;
     display: table-caption;
     ```

  2. float

     ```
     float: left;
     float: right;
     ```

  3. position

     ```
     position: absolute;
     position: fixed;
     ```

  4. overflow

     ```
     overflow: auto;
     overflow: hidden;
     overflow: scroll;
     ```

     ​
