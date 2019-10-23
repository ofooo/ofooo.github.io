---
title: hexo_主题配置
toc: true
date: 2019-02-28 16:49:08
tags:
  - hexo
  - wiki
categories:
  - 编程基础
  - 博客工具
---



### 下载主题

http://theme.typora.io/theme/Law/

下载后把文件夹和.css文件拖动到主题目录中即可



## 配置主题

1. 点击"文件"--->"偏好设置"--->"打开主题目录"
2. 新建一个文件"fish_whitey.css"  内容如下

- 该文件是在whitey.css基础上修改的
- 修改内容有添加注释"/* fish修改"
- 一项是文字内容显示的最大宽度改成了2700, 便于看到更多的文字内容
- 另一项是勾选项的修改从根号改成了圆圈

```css
html {
	font-size: 19px;
}

html, body {
	margin: auto;
	background: #fefefe;
}
body {
	font-family: "Vollkorn", Palatino, Times;
	color: #333;
	line-height: 1.4;
	text-align: justify;
}
#write {
	max-width: 2700px;     /* fish修改: 页面整体尺寸 */
	margin: 0 auto;
	margin-bottom: 2em;
	line-height: 1.53;
	padding-top: 40px;
}


/* fish 修改: 勾选项外观 ---------------------------------------- */
.task-list{
	padding-left: 0;
}

.md-task-list-item {
	padding-left:34px;
}

.md-task-list-item > input{
	width: 1.25rem;
	height: 1.25rem;
	display: block;
	-webkit-appearance: initial;
	top: -0.4rem;   /* 圆圈的高度 */
	margin-left: -1.6em;
	margin-top: calc(1rem - 7px);
	border: none;
}

.md-task-list-item > input:focus{
	outline: none;
	box-shadow: none;
}

.md-task-list-item > input:before{
	border: 1px solid #555;
	border-radius: 1.2rem;  /* 圆圈的大小 */
	width: 1.2rem;
	height: 1.2rem;         
	background: #fff;
	content: ' ';
	transition: background-color 200ms ease-in-out;
	display: block;
}

.md-task-list-item > input:checked:before,
.md-task-list-item > input[checked]:before{
	background: #333;
	border-width: 2px;
	display:inline-block;
	transition: background-color 200ms ease-in-out;
}

.md-task-list-item > input:checked:after,
.md-task-list-item > input[checked]:after {
	opacity: 1;
} 

.md-task-list-item > input:after {
	opacity: 1;
	-webkit-transition: opacity 0.05s ease-in-out;
	-moz-transition: opacity 0.05s ease-in-out;
	transition: opacity 0.05s ease-in-out;
	-webkit-transform: rotate(-45deg);
	-moz-transform: rotate(-45deg);
	transform: rotate(-45deg);
	position: absolute;
	top: 0.27rem;     /* 对号的位置  0.27rem */ 
	left: 0.19rem;     /* 0.19rem */ 
	width: 0.8rem;      /* 对号的大小 */
	height: 0.5rem;
	border: 3px solid #fff;
	border-top: 0;
	border-right: 0;
	content: ' ';
	opacity: 0;
} 
/* fish 修改: 勾选项外观 -   [结束]   --------------------------------------- */


/* Typography
-------------------------------------------------------- */

#write>h1:first-child,
h1 {
	margin-top: 1.6em;
	font-weight: normal;
}

h1 {
	font-size:3em;
}

h2 {
	margin-top:2em;
	font-weight: normal;
}

h3 {
	font-weight: normal;
	font-style: italic;
	margin-top: 3em;
}

h1, 
h2, 
h3{
	text-align: center;
}

h2:after{
	border-bottom: 1px solid #2f2f2f;
    content: '';
    width: 100px;
    display: block;
    margin: 0 auto;
    height: 1px;
}

h1+h2, h2+h3 {
	margin-top: 0.83em;
}

p,
.mathjax-block {
	margin-top: 0;
	-webkit-hypens: auto;
	-moz-hypens: auto;
	hyphens: auto;
}
ul {
	list-style: square;
	padding-left: 1.2em;
}
ol {
	padding-left: 1.2em;
}
blockquote {
	margin-left: 1em;
	padding-left: 1em;
	border-left: 1px solid #ddd;
}
code,
pre {
	font-family: "Consolas", "Menlo", "Monaco", monospace, serif;
	font-size: .9em;
	background: white;
}
.md-fences{
	margin-left: 1em;
	padding-left: 1em;
	border: 1px solid #ddd;
	padding-bottom: 8px;
	padding-top: 6px;
	margin-bottom: 1.5em;
}

a {
	color: #2484c1;
	text-decoration: none;
}
a:hover {
	text-decoration: underline;
}
a img {
	border: none;
}
h1 a,
h1 a:hover {
	color: #333;
	text-decoration: none;
}
hr {
	color: #ddd;
	height: 1px;
	margin: 2em 0;
	border-top: solid 1px #ddd;
	border-bottom: none;
	border-left: 0;
	border-right: 0;
}
.ty-table-edit {
	background: #ededed;
    padding-top: 4px;
}
table {
	margin-bottom: 1.333333rem
}
table th,
table td {
	padding: 8px;
	line-height: 1.333333rem;
	vertical-align: top;
	border-top: 1px solid #ddd
}
table th {
	font-weight: bold
}
table thead th {
	vertical-align: bottom
}
table caption+thead tr:first-child th,
table caption+thead tr:first-child td,
table colgroup+thead tr:first-child th,
table colgroup+thead tr:first-child td,
table thead:first-child tr:first-child th,
table thead:first-child tr:first-child td {
	border-top: 0
}
table tbody+tbody {
	border-top: 2px solid #ddd
}

.task-list{
	padding:0;
}

/* fish修改 注释掉
.md-task-list-item {
	padding-left: 1.6rem;
}

.md-task-list-item > input:before {
	content: '\221A';
	display: inline-block;
	width: 1.33333333rem;
  	height: 1.6rem;
	vertical-align: middle;
	text-align: center;
	color: #ddd;
	background-color: #fefefe;
}

.md-task-list-item > input:checked:before,
.md-task-list-item > input[checked]:before{
	color: inherit;
}
*/

.md-tag {
	color: inherit;
	font: inherit;
}
#write pre.md-meta-block {
	min-height: 35px;
	padding: 0.5em 1em;
}
#write pre.md-meta-block {
	white-space: pre;
	background: #f8f8f8;
	border: 0px;
	color: #999;
	
	width: 100vw;
	max-width: calc(100% + 60px);
	margin-left: -30px;
	border-left: 30px #f8f8f8 solid;
	border-right: 30px #f8f8f8 solid;

	margin-bottom: 2em;
	margin-top: -1.3333333333333rem;
	padding-top: 26px;
	padding-bottom: 10px;
	line-height: 1.8em;
	font-size: 0.9em;
	font-size: 0.76em;
	padding-left: 0;
}
.md-img-error.md-image>.md-meta{
	vertical-align: bottom;
}
#write>h5.md-focus:before {
	top: 2px;
}

.md-toc {
	margin-top: 40px;
}

.md-toc-content {
	padding-bottom: 20px;
}

.outline-expander:before {
	color: inherit;
	font-size: 14px;
	top: auto;
	content: "\f0da";
	font-family: FontAwesome;
}

.outline-expander:hover:before,
.outline-item-open>.outline-item>.outline-expander:before {
  	content: "\f0d7";
}

/** source code mode */
#typora-source {
	font-family: Courier, monospace;
    color: #6A6A6A;
}

.html-for-mac #typora-sidebar {
    -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, .175);
    box-shadow: 0 6px 12px rgba(0, 0, 0, .175);
}

.cm-s-typora-default .cm-header, 
.cm-s-typora-default .cm-property,
.CodeMirror.cm-s-typora-default div.CodeMirror-cursor {
	color: #428bca;
}

.cm-s-typora-default .cm-atom, .cm-s-typora-default .cm-number {
	color: #777777;
}

.typora-node .file-list-item-parent-loc, 
.typora-node .file-list-item-time, 
.typora-node .file-list-item-summary {
	font-family: arial, sans-serif;
}

/* fish修改  注释掉
.md-task-list-item>input {
    margin-left: -1.3em;
    margin-top: calc(1rem - 12px);
}
*/

.md-mathjax-midline {
	background: #fafafa;
}

.md-fences .code-tooltip {
	bottom: -2em !important;
}

.dropdown-menu .divider {
	border-color: #e5e5e5;
}
```

