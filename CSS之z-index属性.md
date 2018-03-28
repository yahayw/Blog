### 简述：
z-index作用的元素：非static定位元素。
z-index的作用：控制元素在z轴上的层叠顺序。
注意点：子元素的z-index值即使设置的天大，如99999，但是子元素在z轴上的层叠高低仍旧受限于"其第一个非static定位的父元素的z-index值"。


### 详细叙述：
在普通文档流中，按照元素的前后顺序，依次从左到右、从上到下的布局页面元素，不会出现一个元素覆盖在另一个元素的上面遮挡住另一个元素的情况（display:relative的元素是特殊例子,display:relative的元素虽然可以设置有效的z-index/top/right/bottom/left，但是相对定位的元素仍然是属于普通文档流的，相对定位元素的真正位置布局是遵从“从左到右、从上到下”的）。
<br/>
<br/>
绝对定位元素和固定定位元素因为脱离了普通文档流，所以不会按照“从左到右、从上到下”的规则来布局，它们的位置布局是由"第一个非static定位的父元素位置"和"top,right,bottom,left属性设置的值"来共同决定，这样带来的结果是：一方面，页面效果更富有层次；另一方面，会带来z轴上的堆叠层级高低的问题考量。
（z轴是指看页面的人眼距离页面的垂直轴）
<br/>
<br/>
堆叠层级的高低是由z-index属性来控制的。z-index属性的值一般为整数，控制元素的堆叠层级高低，一般来说，z-index值越大，层级就越高，越靠近用户的眼睛；
z轴上z-index值更小的元素会在z-index值更大的元素的下面，离人眼更远。 **`z-index:auto;`的元素不会参与层级高低的比较**
<br/>
<br/>
z-index属性的作用规则：一般来说z-index越大，堆叠层级越高，越靠近人眼，但是...看下面
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

 ![结果如图，注意元素的层叠顺序](https://github.com/yahayw/Blog/blob/master/blog-imgs/z-index.PNG)
    看看上图结果，为什么明明 元素child1的z-index值 比 child1的z-index值 大,元素child1的层级却比元素child2的层级要低呢？
    <br/>
    答案的关键在于，**两个子元素的 非static父元素的 z-index值的比较**，.parent1和.parent2的z-index值相等，那么按照布局顺序会导致.paret2在.parent1的上面，由此带来的影响是，.parent2的子元素.child2会在.parent1的子元素.child1的上面，这就类似父代拥有的"优势"“继承”给了孩子。
    <br/>
    现在，我们想要让.parent1比.parent2更靠近人眼，该用什么办法？
    <br/>
    我想到了2个方法：
    <br/>
    1.改变DOM顺序
    <br/>
    ```
    <div class="parent2">
      <div class="child2"></div>
    </div>
    <div class="parent1">
      <div class="child1"></div>
    </div>
    ```
    <br/>
    2.parent2的z-index值 设置得 比parent1大，如
    <br/>
    ```
	.parent1 {
		z-index: 2;
	}
	.parent2 {
		z-index: 1;
	}
    ```
    <br/>
