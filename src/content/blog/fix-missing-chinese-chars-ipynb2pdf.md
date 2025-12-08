---
title: 解决.ipynb转PDF中文字符缺失的问题
description: 介绍了三种解决 nbconvert 转换 PDF 时中文字符无法显示的方法。
publishDate: 2025-12-08
---

在使用 Jupyter Notebook 进行数据分析或报告撰写时，将 `.ipynb` 文件转换为 PDF 是常见需求。然而，在使用默认命令 `nbconvert --to pdf` 时会发现，所有的中文字符都消失了。

这是因为默认转换引擎（LaTeX）的模板未配置中文字体支持。下文总结一下三种行之有效的解决方案。

## 1. 现代化首选 —— 使用 `webpdf`

这是目前最优雅的解决方案。它的原理是先将 Notebook 渲染为网页，再利用 Headless Browser 将其“打印”为 PDF。这种方式能完美保留网页上的所有排版、图表和中文字体，且无需复杂的 LaTeX 配置。

**操作步骤：**

1.  安装支持库：

    ```bash
    pip install nbconvert[webpdf]
    ```

    *(注：首次运行可能需要下载 Chromium 驱动)*

2.  执行转换：

    ```bash
    jupyter nbconvert --to webpdf your_notebook.ipynb
    ```

## 2. 极简应急 —— 转 HTML 后打印

如果不想安装额外的 Python 库，或者只是偶尔需要转换，这是最快的方法。

**操作步骤：**

1.  将 Notebook 导出为 HTML：

    ```python
    jupyter nbconvert --to html your_notebook.ipynb
    ```

2.  用浏览器打开生成的 HTML 文件。

3.  使用浏览器的“打印”功能 (`Ctrl+P` / `Cmd+P`)，目标打印机选择 **“另存为 PDF”**。

## 3. 学术排版 —— 配置 LaTeX 引擎

由于 LaTeX 默认不支持 CJK 字符，因此需要改用 `xelatex` 引擎并指定系统字体。

**操作步骤：**

1.  转换为 LaTeX 源码：

    首先生成 .tex 文件，而不是直接生成 PDF。

    ```python
    jupyter nbconvert --to latex your_notebook.ipynb
    ```

2.  修改 .tex 文件：

    打开生成的 .tex 文件，在文档头部（`\documentclass` 之后，`\begin{document}` 之前）加入以下配置。并根据操作系统选择正确的字体：

    ```latex
    \usepackage{xeCJK}
    
    % --- Windows 用户 ---
    % \setCJKmainfont{SimSun} % 设置为宋体
    
    % --- macOS 用户 ---
    \setCJKmainfont{PingFang SC} % 设置为苹方-简
    ```

3.  编译生成 PDF：

    在终端中使用 xelatex 命令编译（需安装 TeX Live 或 MiKTeX 环境）：

    ```bash
    xelatex your_notebook.tex
    ```