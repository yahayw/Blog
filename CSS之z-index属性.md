z-index属性作用：
<br/>
z-index作用元素：
<br/>
z-index属性的作用规则：
<br/>
  代码示范：
  <br/>
  
    ```    
    <!--HTML主要代码-->
    <div class="parent1">
      <div class="child1"></div>
    </div>
    <div class="parent2">
      <div class="child2"></div>
    </div>
    /*CSS主要代码*/
	.parent1,
	.parent2,
	.child1,
	.child2 {
	position: absolute;      
	}
	.parent1 {
		z-index: 1;
	}
	.parent2 {
		z-index: 1;
	}
	.child1 {
		z-index: 200;
	}
	.child2 {
		z-index: 100;
	}
    ```

 ![结果如图，注意元素的层叠顺序]("./blog-imgs/z-index.png")
    
