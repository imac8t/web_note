**`目录`**

- [安装、使用sass&compass](#安装、使用sass&compass)
	+ [安装](#安装)
	+ [使用](#使用)

- [sass常用语法](#sass常用语法)
	+ [声明变量](#声明变量)
	+ [语法嵌套](#语法嵌套)
	+ [声明混合宏](#声明混合宏)
	+ [继承](#继承)
	+ [占位符%](#占位符%)
	+ [注意事项](#混合宏 VS 继承 VS 占位符)

- [视频教程]()
	+ [sass(1小时33分)](http://www.imooc.com/learn/364)
	+ [compass(2小时41分)](http://www.imooc.com/learn/371)

---

<h2 id="安装、使用sass&compass">安装、使用sass&compass</h2> 


<h4 id="安装">安装</h4> 
> 使用cmd指令前先安装[ruby(windows版)](http://rubyinstaller.org/downloads/)

cmd指令|说明
-----|-----
gem sources --remove https://rubygems.org/ | 移除旧源（国内网络原因）
gem sources -a https://ruby.taobao.org/ | 添加淘宝源
gem sources -l | 查看当前现有源
gem install sass | 安装[sass](http://sass-lang.com/)
gem install sass --version=3.3.0 | 安装指定版本sass
gem list | 列出gem本地所有程序包
gem uninstall sass --version=3.3.0 | 删除指定版本sass
gem install compass | 安装[compass](http://compass-style.org/reference/compass/)
gem install compass-normalize | 安装normalize插件（sass语法增强）	


<h4 id="使用">使用</h4> 
> 指定目录下打开cmd窗口使用指令。

windows系统写代码过程转译会有乱码或报错的情况，找到engine.rb文件（一般位于Ruby22\lib\ruby\gems\2.2.0\gems\sass-3.4.18\lib\sass目录下面），在所有的require后面新增如下代码：**Encoding.default_external = Encoding.find('utf-8')**

cmd指令 | 说明
-----|-----
compass create 文件名 | 在指定文件夹创建compass目录
sass main.cscc main.css | 转译scss文件（scss/sass文件目录下使用）
compass watch | 实时监听scss文件，自动转译（compass根目录下）
compass compile | 输出css,配置在config.rb中（例压缩模式：13行中添加output_style = :compressed）


---
<h2 id="sass常用语法">sass常用语法</h2> 


<h6 id="声明变量"> ·声明变量</h6>

```sass
$width:500px;
```	  


<h6 id="声明默认变量"> ·声明默认变量</h6>

```sass
$width:500px !default;
```

> 默认变量用来设置默认变量，根据需求覆盖，覆盖时重新声明默认变量即可	  


<h6 id="语法嵌套"> ·语法嵌套</h6>

```sass
a {
  	color：red;
      	&:before {
     	content:””
  	}
  	body & {
		color:blue;
  	}
}
```	  


<h6 id="声明混合宏"> ·声明混合宏</h6>
```sass
@mixin border-radius($radius) {
	-webkit-border-radius:$radius;
	border-radius:$radius;
}
```
> $radius也可以给一个默认值，如@mixin border-radius($radius:50%)

调用混合宏
```sass
button {
	@include border-radius(5px);
}
```	  


<h6 id="多个参数的混合宏"> ·多个参数的混合宏</h6>
```sass
@mixin center($width,$height){
	width: $width;
	height: $height;
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -($height) / 2;
	margin-left: -($width) / 2;
}
```

调用
```sass
div {
	@include center;
}
```
> 混合宏的缺点是会造成过多冗余的代码，sass不会智能合并  


<h6 id="继承"> ·继承</h6>
```sass
.btn {
	border: 1px solid #ccc;
	padding: 6px 10px;
	font-size: 14px;
}

.btn-primary {
	background-color: #f36;
	color: #fff;
	@extend .btn; //继承.btn所有属性
}
```	  


<h6 id="占位符%"> ·占位符%</h6>
```sass
%mt5 { margin-top: 5px; }
%pt5{ padding-top: 5px; }

.btn {
	@extend %mt5;
	@extend %pt5;
}

.block {
@extend %mt5;
	span {
		@extend %pt5;
	}
}

```
输出结果：
```css
.btn, .block { margin-top: 5px; }
.btn, .block span { padding-top: 5px; }
```
> %placeholder 声明的代码，如果不被 @extend 调用的话，不会产生任何代码。与$不同的是它可以合并代码。  	  


<h6 id="混合宏 VS 继承 VS 占位符"> ·混合宏 VS 继承 VS 占位符</h6>
- 如果你的代码块中涉及到变量，建议使用混合宏来创建相同的代码块；
- 如果不需要任何参数，且有一个基类已在文件中存在，那么建议使用 Sass 的继承。  	  


<h6 id="注释"> ·注释</h6>
//不会被编译，/**/会被编译  	  
	

<h6 id="运算"> ·运算</h6>
- 被乘除数后不能加单位；
- 减号前面要加空格，除号/要在公式外加括号（）；
- 复杂的公式同正常数学一样用（）表明先后  