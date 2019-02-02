# Attack_On_D3
D3 learning...

进击的D3.js！！！
https://d3js.org/

D3 
Data-Driven Documents
一个 JavaScript 的函数库
主要是用来做数据可视化的。

1.如何学习和使用 D3
a.官方网站：包含有很多示例和 API
http://d3js.org/

b.Mike Bostock 的博客和作品展示板
http://bost.ocks.org/mike/

2.如何在js中使用D3.js
D3 是一个 JavaScript library，不需要任何安装，fecth or include 在网页就好。
两种方法：
a.下载 D3.js 的文件
d3.zip
解压后，在 HTML 文件中包含相关的 js 文件即可。
b.CDN 引用：更简单，但要保持网络通畅
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>

3.相比于JS的优势
D3.js 中的所有功能在 JavaScript 中都能实现，但D3的操作像JQuery一样，让JS操作更为简单直观。
examples：
js-修改html中节点的内容
<html> 
  <head> 
        <meta charset="utf-8"> 
        <title>HelloWorld</title> 
  </head> 
    <body> 
    <p>a</p>
    <p>b</p>
        <script>
        var paragraphs = document.getElementsByTagName("p");
        for (var i = 0; i < paragraphs.length; i++) {
          var paragraph = paragraphs.item(i);
          paragraph.innerHTML = "hello";
        }          
        </script> 
    </body> 
</html>
D3则简单很多
      <html> 
  <head> 
        <meta charset="utf-8"> 
        <title>HelloWorld</title> 
  </head> 
    <body> 
        <p>a</p>
        <p>b</p>
        <script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script> 
        <script>  
        d3.select("body").selectAll("p").text("hello");      
        </script> 
    </body> 
</html>

如果要改变P的CSS：
var p = d3.select("body")
          .selectAll("p")
          .text("hello world");
p.style("color","red")
 .style("font-size","72px");

4. 具体语法
4.1选择元素
在 D3 中，用于选择元素的函数有两个，这两个函数返回的结果称为选择集。
这两个函数都符合 CSS 选择器的条件的，即用“井号（#）”表示 id，用“点（.）”表示 class。
d3.select()：是选择所有指定元素的第一个
d3.selectAll()：是选择指定元素的全部

a.选择集的常见用法如下：
var body = d3.select("body"); //选择文档中的body元素
var p1 = body.select("p");      //选择body中的第一个p元素
var p = body.selectAll("p");    //选择body中的所有p元素
var svg = body.select("svg");   //选择body中的svg元素
var rects = svg.selectAll("rect");  //选择svg中所有的svg元素

b.选择其中某个元素
使用id 定位这个元素，然后使用select 选择元素。
var p = body.select("#idOfP");
p.style("color","red");

c.选择某一部分元素
给这部分元素添加同一个class，然后用 selectAll（由于需要选择多个元素）。
<p class="myclass">a</p>
<p class="myclass">b</p>

var p = body.selectAll(".classOfP");
p.style("color","red");


d.对于已经绑定了数据的选择集，还有一种选择元素的方法， function(d, i)
其中两个参数
d 代表数据，也就是与某元素绑定的数据。
i 代表索引，代表数据的索引号，从 0 开始。


4.2绑定数据
D3 能将数据绑定到 DOM 上，它是通过以下两个函数来绑定数据的：
datum()：绑定一个数据到选择集上
data()：绑定一个数组到选择集上，数组的各项值分别与选择集的各元素绑定
相对而言，data() 比较常用。

example:假设现在有三个段落元素
<p>A</p>
<p>B</p>
<p>C</p>
var dataset = ["dog","cat","Lion"];
var body = d3.select("body");
var p = body.selectAll("p");

p.data(dataset)
  .text(function(d, i){
      return d;
  });
  
4.3插入元素
插入元素涉及的函数有两个：
append()：在选择集末尾插入元素
insert()：在选择集前面插入元素

Examples：
append()：在 body 的末尾添加一个 p 元素，结果为：
body.append("p")
    .text("append p element");

insert()：在 body 中 id 为 myid 的元素前添加一个段落元素。
body.insert("p","#idOfP")
  .text("insert p element");

4.3删除元素
删除一个元素时，对于选择的元素，使用 remove 即可，例如：
var p = body.select("#idOfP");
p.remove();

