---
title: Angular规范的git-commit-message
typora-root-url: ./Angular规范的git-commit-message
date: 2021-10-22 15:35:26
tags:
---

### 介绍

>Git 每次提交代码，都要写 Commit message（提交说明），否则就不允许提交。
>
>```bash
>$ git commit -m "hello world"
>```
>
>上面代码的`-m`参数，就是用来指定 commit mesage 的。
>
>如果一行不够，可以只执行`git commit`，就会跳出文本编译器，让你写多行。
>
>```bash
>$ git commit
>```
>
>原则上是写什么都行的。
>
>但是一般来说，commit message 应该清晰明了，说明本次提交的目的。
>
>目前，社区有多种 Commit message 的[写法规范](https://github.com/ajoslin/conventional-changelog/blob/master/conventions)。本文介绍[Angular 规范](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit?spm=a2c6h.12873639.0.0.7ff92ae72HmL6b#heading=h.greljkmo14y0)（见上图），这是目前使用最广的写法，比较合理和系统化，并且有配套的工具。

### 格式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

```
<type>(<scope>): <subject>// 空一行<body>// 空一行<footer>
```

其中，Header 是必需的，Body 和 Footer 可以省略。

不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

### 2.1 Header

Header部分只有一行，包括三个字段：`type`（必需）、`scope`（可选）和`subject`（必需）。

**（1）type**

`type`用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

如果`type`为`feat`和`fix`，则该 commit 将肯定出现在 Change log 之中。其他情况（`docs`、`chore`、`style`、`refactor`、`test`）由你决定，要不要放入 Change log，建议是不要。

**（2）scope**

`scope`用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

**（3）subject**

`subject`是 commit 目的的简短描述，不超过50个字符。

- 以动词开头，使用第一人称现在时，比如`change`，而不是`changed`或`changes`
- 第一个字母小写
- 结尾不加句号（`.`）

### 2.2 Body

Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

```bash
More detailed explanatory text, if necessary.  Wrap it to 
about 72 characters or so. Further paragraphs come after blank lines.- Bullet points are okay, too- Use a hanging indent
```

有两个注意点。

（1）使用第一人称现在时，比如使用`change`而不是`changed`或`changes`。

（2）应该说明代码变动的动机，以及与以前行为的对比。

### 2.3 Footer

Footer 部分只用于两种情况。

**（1）不兼容变动**

如果当前代码与上一个版本不兼容，则 Footer 部分以`BREAKING CHANGE`开头，后面是对变动的描述、以及变动理由和迁移方法。

```
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

**（2）关闭 Issue**

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

```
Closes #234
```

也可以一次关闭多个 issue 。

```
Closes #123, #245, #992
```

### 2.4 Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以`revert:`开头，后面跟着被撤销 Commit 的 Header。

```
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

Body部分的格式是固定的，必须写成`This reverts commit <hash>.`，其中的`hash`是被撤销 commit 的 SHA 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的`Reverts`小标题下面。



>参考：
>
>[Git 提交的正确姿势：Commit message 编写指南-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/441408)

