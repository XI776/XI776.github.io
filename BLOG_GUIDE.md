# 博客维护说明

本站继续使用 Hexo。文章在 `source/_posts/`，主题设置在根目录的 `_config.butterfly.yml`，自定义排版在 `source/css/blog.css`。

## 新增文章和分类

在项目根目录运行 `npx hexo new post "文章标题"`，然后编辑生成的 Markdown 文件。文件顶部可以这样写：

```yaml
---
title: 文章标题
date: 2026-10-27 12:00:00
categories: 新分类名称
description: 一句真实的文章简介，用于首页列表。
---
```

标题和日期会由新建命令自动填写。写入一个新的 `categories` 名称后，Hexo 会自动生成该分类页，分类总览和侧栏也会自动出现它；不需要修改导航代码。分类名称建议保持简短、稳定。要调整旧文章的分类，只需修改那篇文章的 `categories` 值。当前文章模板不预设标签；以后如需标签，可自行添加 `tags` 字段。

在第二条 `---` 后写正文。用 `## 小标题` 形成文章目录；代码块以三个反引号加语言名开头，结尾再写三个反引号。例如：

````md
```cpp
#include <iostream>
int main() { return 0; }
```
````

## 图片与链接

公共图片放在 `source/images/`，文章中使用 `/images/文件名` 引用。原有文章文件名和 `_config.yml` 的 `permalink` 规则保持不变，修改标题或分类不会改变旧文章地址。若要改文章文件名或日期，先考虑旧链接跳转。

## 本地预览

```sh
npm run build
npm run server -- --port 4000
```

打开 `http://localhost:4000/`。搜索索引会随构建自动生成。深浅色切换、文章目录、macOS 风格代码块、代码复制，以及文章字数和阅读时长由 Butterfly 主题提供。

预览服务已运行时，保存文章并刷新浏览器即可；不要重复启动同一个端口。发布到 GitHub 前，先核对 `_config.yml` 中的 `deploy.repo` 是否为实际仓库地址。

## 当前分类

- C++ 面向对象
- C++ 基础与标准库
- 博客搭建与随笔
- JavaScript 片段

正文为空的旧文章也保留了原文件与旧链接；后续可以直接补写。
