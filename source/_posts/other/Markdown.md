---
title:  Markdown 编辑器语法指南
tags:  [md]
categories:  [工具]
date:  2018-06-11 16:17:22
---




[Markdown 编辑器语法指南](https://segmentfault.com/markdown/)

[MacDown](http://macdown.uranusjr.com/)


## 代码高亮

如果你只想高亮语句中的某个函数名或关键字，可以使用 `function_name()` 实现
通常编辑器根据代码片段适配合适的高亮方法，但你也可以用 以下方式 包裹一段代码，并指定一种语言

``` javascript
$(document).ready(function () {
    alert('hello world');
});

```

>
支持的语言：1c, abnf, accesslog, actionscript, ada, apache, applescript, arduino, armasm, asciidoc, aspectj, autohotkey, autoit, avrasm, awk, axapta, bash, basic, bnf, brainfuck, cal, capnproto, ceylon, clean, clojure, clojure-repl, cmake, coffeescript, coq, cos, cpp, crmsh, crystal, cs, csp, css, d, dart, delphi, diff, django, dns, dockerfile, dos, dsconfig, dts, dust, ebnf, elixir, elm, erb, erlang, erlang-repl, excel, fix, flix, fortran, fsharp, gams, gauss, gcode, gherkin, glsl, go, golo, gradle, groovy, haml, handlebars, haskell, haxe, hsp, htmlbars, http, hy, inform7, ini, irpf90, java, javascript, json, julia, kotlin, lasso, ldif, leaf, less, lisp, livecodeserver, livescript, llvm, lsl, lua, makefile, markdown, mathematica, matlab, maxima, mel, mercury, mipsasm, mizar, mojolicious, monkey, moonscript, n1ql, nginx, nimrod, nix, nsis, objectivec, ocaml, openscad, oxygene, parser3, perl, pf, php, pony, powershell, processing, profile, prolog, protobuf, puppet, purebasic, python, q, qml, r, rib, roboconf, rsl, ruby, ruleslanguage, rust, scala, scheme, scilab, scss, smali, smalltalk, sml, sqf, sql, stan, stata, step21, stylus, subunit, swift, taggerscript, tap, tcl, tex, thrift, tp, twig, typescript, vala, vbnet, vbscript, vbscript-html, verilog, vhdl, vim, x86asm, xl, xml, xquery, yaml, zephir


## markdown

```markdown
<b> Markdown 在此处同样适用，如 *加粗* </b>

- 列表文本前使用 [减号+空格]
+ 列表文本前使用 [加号+空格]
* 列表文本前使用 [星号+空格]

> 引用文本前使用 [大于号+空格]
> 折行可以不加，新起一行都要加上哦

> 
> > 最外层引用
> > 多一个 > 嵌套一层引用
> > > 可以嵌套很多层


![图片名称](http://图片网址)

```

## 分隔符
---

如果你有写分割线的习惯，可以新起一行输入三个减号-。前后都有段落时，请空出一行：

``` markdown
前面的段落

---

后面的段落

```