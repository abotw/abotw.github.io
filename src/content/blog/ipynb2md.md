---
title: 告别复制粘贴：从 Jupyter Notebook 转换到 Markdown 的完全指南
description: 介绍了如何通过官方工具 Nbconvert、界面导出以及 Jupytext 这三种方式，将 Jupyter Notebook（.ipynb） 文件高效、干净地转换成 Markdown（.md） 格式。
publishDate: 2025-12-08
---

手动复制粘贴进行格式转换不仅效率低，代码高亮和图片路径还容易出错。下文介绍三种将 `.ipynb` 转换为 `.md` 的方法，覆盖从“小白”到“极客”的所有需求。

## 1. 官方命令行神器 —— Nbconvert

**适合场景：** 需要批量转换、自动化脚本、或者对图片输出有要求。

`nbconvert` 是 Jupyter 生态系统自带的工具，也是最标准的转换方式。它不仅能转 Markdown，还能转 HTML、PDF 等。

### 1.1 基础用法

在终端（Terminal）或命令行中运行以下命令：

```python
jupyter nbconvert --to markdown your_notebook.ipynb
```

运行后，会得到一个 `your_notebook.md` 文件。

### 1.2 进阶技巧：处理图片

默认情况下，转换后的图片会以 Base64 编码直接嵌入 Markdown 文件中，导致文件体积巨大且不利于编辑器预览。

如果希望**将图片提取到单独的文件夹**，可以使用以下命令：

```bash
jupyter nbconvert --to markdown your_notebook.ipynb --NbConvertApp.output_files_dir=images
```

>   **提示：** 这会自动创建一个名为 `images` 的文件夹，并将 Markdown 中的图片链接指向该文件夹。

## 2. 所见即所得 —— GUI

**适合场景：** 偶尔转换单个文件，不想敲命令。

Jupyter Lab 和 VS Code 都内置了导出功能。

### 2.1 Jupyter Notebook / Lab

-   打开 `.ipynb` 文件。
-   点击菜单栏的 **File (文件)**。
-   选择 **Save and Export Notebook As (另存并导出为)...**
-   选择 **Markdown**。

浏览器会自动下载转换好的压缩包（包含 `.md` 文件和图片文件夹）。

### 2.2 VS Code

-   在 VS Code 中打开 `.ipynb` 文件。
-   点击编辑器右上角的 **... (更多操作)** 按钮。
-   选择 **Export (导出)**。
-   选择 **Markdown**。

## 3. 双向同步黑科技 —— Jupytext

**适合场景：** 版本控制（Git）、习惯在 Markdown 中写代码。

`Jupytext` 是一个极其强大的插件。它不仅能转换，还能让 `.ipynb` 和 `.md` 文件保持**实时双向同步**。这意味着可以在 Markdown 中修改文字，在 Notebook 中运行代码，两者互不干扰。

### 3.1 安装

```python
pip install jupytext
```

### 3.2 用法

在命令行中配对文件：

```python
jupytext --set-formats ipynb,md your_notebook.ipynb
```

或者直接转换：

```python
jupytext --to md your_notebook.ipynb
```

使用 Jupytext 生成的 Markdown 非常干净，没有冗余的输出元数据，非常适合提交到 GitHub。

## 4. 总结

| **工具**      | **优点**                     | **缺点**                   | **推荐人群**           |
| ------------- | ---------------------------- | -------------------------- | ---------------------- |
| **Nbconvert** | 官方自带，功能最全，支持批量 | 需要敲命令                 | 开发者、需要批量处理   |
| **GUI 导出**  | 简单直观，无需配置           | 每次只能转一个，且步骤繁琐 | 偶尔转换的用户         |
| **Jupytext**  | 双向同步，Git 友好，格式干净 | 需要单独安装               | Git 重度用户、博客作者 |

