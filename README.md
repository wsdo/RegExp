# 正则基础知识点![image](https://cloud.githubusercontent.com/assets/18028533/21600946/ce4ef7ea-d1be-11e6-9052-1a202764043f.png)
![image](https://cloud.githubusercontent.com/assets/18028533/21600997/73f8b56e-d1bf-11e6-8a12-64b5afea78dc.png)
- [正则构建工具一](https://regexper.com/)
- [正则构建工具二](https://www.debuggex.com/)
- [正则基础知识点](https://github.com/Kelichao/RegExp/issues/1)
- [正则demo](http://www.softwhy.com/zhengzeshili/)
- [点击链接豆瓣网友的回答\r\n的区别](https://www.douban.com/note/328054605/?type=like)

# 1.元字符
 _元字符是在正则表达式中有特殊含义的非字母字符（注 ”-“ 除外）_
 
> 元意文本字符

<table>
<tr>
<td>序号</td><td>符号</td><td>序号</td><td>符号</td>
</tr>
<tr>
	<td>1. </td><td>* </td><td>2. </td><td>+ </td>
</tr>
<tr>
	<td>3.</td> <td>?</td><td>4.</td> <td>$</td>
</tr>
<tr>
	<td>5.</td> <td>^</td><td>6.</td> <td>.</td>
</tr>
<tr>
	<td>7.</td> <td>|</td><td>8.</td> <td>\</td>
</tr>
<tr>
	<td>9.</td> <td>(</td><td>10.</td> <td>)</td>
</tr>
<tr>
	<td>11.</td> <td>{</td><td>12.</td> <td>}</td>
</tr>
<tr>
	<td>13.</td> <td>[</td><td>14.</td> <td>]</td>
</tr>
</table>

> 特殊的元字符

<table>
	<tr><td>1. </td><td>\t 水平制表符</td></tr>
<tr><td>2. </td><td>\v 垂直制表符</td></tr>
<tr><td>3. </td><td>\n 换行符(真正起作用的换行符)</td></tr>
<tr><td>4. </td><td>\r 回车符(回车符实际意义是到行的开头)</td></tr>
<tr><td>5. </td><td>\0 空字符</td></tr>
<tr><td>6. </td><td>\f 换页符</td></tr>
<tr><td>7. </td><td>\cX 与X对应的控制字符（Ctrl+X）</td></tr>
</table>

```javascript
var x ="aaaaaaa\nbbbbbbb";
console.log(x);
```

>  \r\n表示回车换行（所以我们一般使用的回车键是\r\n）

> 我们在平时使用电脑时，已经习惯了回车和换行一次搞定，敲一个回车键，即是回车，又是换行。



# 2.字符类

> 中括号里面字符与字符之间代表的是或，把a|b|c都替换

```javascript
var regExp = "a1b2c3d4".replace(/[abc]/g, "X")
//  得到 "X1X2X3d4"
```

> 反向类[^] ：把abc以外的字符都替换
 
```js
var regExp = "a1b2c3d4".replace(/[^abc]/g, "X")
//  得到 "aXbXcXXX"
```

> 范围类 [a-z]：替换a-z的字符

```javascript
var regExp = "a1b2d3x4z9".replace(/[a-z]/g, "Q")
//  得到 "Q1Q2Q3Q4Q9"
```

> 连写

```js
var regExp = "a1b2d3x4z9AAAA".replace(/[a-zA-Z]/g, "Q")
//  得到 "Q1Q2Q3Q4Q9QQQQ"
```

# 3. 预定义类

> 其实就是已经帮你写好的类

<table>
	<tr>
		<td>字符</td>
		<td>等价类</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>.</td>
		<td>[^\r\n]</td>
		<td>除了回车符和换行符之外的所有字符</td>
	</tr>
	<tr>
		<td>\d</td>
		<td>[0-9]</td>
		<td>数字字符</td>
	</tr>
	<tr>
		<td>\D</td>
		<td>[^0-9]</td>
		<td>非数字字符</td>
	</tr>
	<tr>
		<td>\s</td>
		<td>[\t\n\xOB\f\r]</td>
		<td>空白符</td>
	</tr>
	<tr>
		<td>\S</td>
		<td>[^\t\n\xOB\f\r]</td>
		<td>非空白符</td>
	</tr>
	<tr>
		<td>\w</td>
		<td>[a-zA-Z_0-9]</td>
		<td>单词字符（字母、数字下划线）</td>
	</tr>
	<tr>
		<td>\W</td>
		<td>[^a-zA-Z_0-9]</td>
		<td>非单词字符</td>
	</tr>
</table>

> 优势，精简

```javascript
// 匹配一个abc + 数字 + 任意字符
var regExp = /abc[0-9][^\r\n]/;
var regExp2 = /abc\d./;
```

# 4. 边界

> 边界属于定位符

<table>
	<tr>
		<td>字符</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>^</td>
		<td>以***开始</td>
	</tr>
	<tr>
		<td>$</td>
		<td>以***结束</td>
	</tr>
	<tr>
		<td>\b</td>
		<td>单词边界</td>
	</tr>
	<tr>
		<td>\B</td>
		<td>非单词边界</td>
	</tr>
</table>

> ^,$例子

```js
var reg = /^abc/g;
console.log("abcabcabcabc".replace(reg,"111"));// 111abcabcabc

var reg = /abc$/g;
console.log("abcabcabcabc".replace(reg,"111"));// abcabcabc111
```
## m换行标志在这种地方有用，处理多行
![image](https://cloud.githubusercontent.com/assets/18028533/19920433/92835dc2-a113-11e6-89f6-dc1966bd549d.png)

# 5.量词

> 出现次数

```javascript
// 匹配数字20次
var regExp = /\d{20}/ 
```
<table>
	<tr>
		<td>字符</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>?</td>
		<td>出现一次或者多次（最多出现一次）</td>
	</tr>
	<tr>
		<td>+</td>
		<td>出现一次或者多次（至少出现一次）</td>
	</tr>
	<tr>
		<td>*</td>
		<td>出现零次或多次（任意次）</td>
	</tr>
	<tr>
		<td>{n}</td>
		<td>出现n次</td>
	</tr>
	<tr>
		<td>{n,m}</td>
		<td>出现n到m次</td>
	</tr>
	<tr>
		<td>{n,}</td>
		<td>至少出现n次</td>
	</tr>
</table>

# 6.贪婪模式

> 正则默认就是贪婪模式

```javascript
var regExp = "12345678".replace(/\d{3,6}/g, "X")
//  得到 "X78" 把123456都匹配了
```
# 7.非贪婪模式

>  在量词后面加?即可

```javascript
var regExp = "12345678".replace(/\d{3,6}?/g, "X")
//  得到 "XX78" 把123,456都匹配了
```

# 8. 正则中的或 "|"
> 例一

```js
var regExp = "aaabbb".replace(/aaa|bbb/g, "X");
//  得到 "XX" ,没有括号就是全局
```
> 例二

```js
var regExp = "aaabbdddaaaccddd".replace(/aaa(bb|cc)ddd/g, "X");
//  得到 "XX"
```

# 9.分组 "()"

> 量词如果不跟分组一起使用只能度量一个字符

```javascript
var regExp = "a1b2c3d4".replace(/([a-z]\d){3}/g, "X");
//  得到 "Xd4" 
```

# 10.捕获/子表达式

> 例如:把2015-12-25 => 12/25/2015

- 捕获的话可以用于位置交换。
```js
var regExp = "2015-12-25".replace(/(\d{4})-(\d{2})-(\d{2})/g, "$3/$2/$1");
//  得到 "25/12/2015" 
```

> 注意：如果用replace方法会把没有匹配到的字符

```js
// replace方法会把没有匹配到的字符，会拼接到子表达式后面
// 得到aaabbbccc原字符串 
// 其实是 aaa + bbbccc(原字符串没有拼接到的多余字符)
"aaabbbccc".replace(/(aaa)/g, "$1");// aaabbbccc
```

- 捕获的顺序

> 对于括号里面嵌套的括号，其实$1,$2是被用掉了的。

```js
var reg = /(^("|'))(\w+)("$)/g;
console.log("\"123abc\"".replace(reg, "$1"));// "
console.log("\"123abc\"".replace(reg, "$2"));// "
console.log("\"123abc\"".replace(reg, "$3"));// 123abc
```

**如果不希望被捕获，则进行忽略分组**
`(:?cont)`

# 10. 前瞻（JS不支持后顾）
> 注意 前瞻与忽略子表达式不同，前瞻会将已匹配的字符纳入已经匹配
<table>
	<tr>
		<td>名称</td>
		<td>正则</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>正向前瞻</td>
		<td>exp(?=assert)</td>
		<td>如果前方匹配到这个</td>
	</tr>
	<tr>
		<td>负向前瞻</td>
		<td>exp(?!assert)</td>
		<td>如果前方匹配不到这个</td>
	</tr>
	<tr>
		<td>正向后顾</td>
		<td>exp(?<=assert)</td>
		<td>JavaScript不支持</td>
	</tr>
	<tr>
		<td>负向后顾</td>
		<td>exp(?< !assert)</td>
		<td>JavaScript不支持</td>
	</tr>
</table>

> 注：前瞻只能放在正则的最后位置，后顾要放在正则最前面的位置

> 前瞻与不希望被捕获的区别是不会将前瞻表达块归于匹配对象，而捕获是归属于匹配对象的

```js
var regExp = "a2*3".replace(/\W(?=\d)/g, "X");
//  得到 "a2X3" 

var x = "report=ccccc11111&&&ddddd=555555&eeeee=66666";
reg =/report=(?=ccc{3})/gi;
console.log(x.match(reg));// ["report="]
```
> 负向前瞻

- 语法为（?!pattern）,在被搜索字符串的相应位置不能有pattern部分表示的内容，也不将其作为匹配结果进行处理，当然也不会存储在缓冲区。

# 11.反向捕获

```javascript
var regExp = "1aa1".replace(/(\d)(\D)\2\1/g, "X")
//  得到 "X" 
```
