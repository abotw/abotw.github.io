---
title: Pandoc 入门：通用文档转换器
description: 介绍了Pandoc的安装、核心转换命令和利用元数据、引用文档来自定义输出格式的进阶技巧。
publishDate: 2025-12-07
---

在进行文档撰写的过程中，有时候会遇到需要转换不同格式文档的问题，Pandoc 就是一个很好用的工具。

Pandoc 被誉为“文档转换的瑞士军刀”，它是一款强大的命令行工具，能够识别几十种输入格式并输出几十种输出格式。

## 1. 什么是 Pandoc？

简单来说，Pandoc 是一个开源的程序，它能够将一种标记语言或文档格式转换为另一种。它的核心工作原理是将输入文档解析成一个抽象的**内部文档模型**（Abstract Syntax Tree, **AST**），然后将这个 AST 渲染成目标格式。

## 2. 安装 Pandoc

-   **Windows:** 通常推荐下载安装包（`.msi` 文件）。

-   **macOS:** 使用 Homebrew 进行安装：

    ```bash
    brew install pandoc
    ```

-   **Linux (Debian/Ubuntu):** 使用系统的包管理器进行安装：

    ```bash
    sudo apt-get install pandoc
    ```

安装完成后，在终端或命令提示符中输入 `pandoc --version`，如果能看到版本信息，说明安装成功了。

## 3. 一次简单的转换

Pandoc 的基本用法非常简单。假设有一个名为 `my_document.md` 的 Markdown 文件，想把它转换为一个 Word 文档（`.docx`）：

```bash
pandoc my_document.md -o my_document.docx
```

-   `pandoc`: 程序的名称。
-   `my_document.md`: 输入文件。
-   `-o my_document.docx`: 指定输出文件名 (`-o` 是 `--output` 的缩写)。

## 4. 常见转换示例

Pandoc 支持的格式非常多，以下列举一些最常用的转换：

| **转换目标**                                | **命令示例**                     |
| ------------------------------------------- | -------------------------------- |
| **Markdown** $\rightarrow$ **HTML**         | `pandoc input.md -o output.html` |
| **Markdown** $\rightarrow$ **PDF**          | `pandoc input.md -o output.pdf`  |
| **Markdown** $\rightarrow$ **LaTeX**        | `pandoc input.md -o output.tex`  |
| **Word (.docx)** $\rightarrow$ **Markdown** | `pandoc input.docx -o output.md` |
| **HTML** $\rightarrow$ **Markdown**         | `pandoc input.html -o output.md` |

## 5. 让文档更专业

### 5.1 使用元数据 (Metadata)

可以通过在 Markdown 文件顶部添加一个 YAML 元数据块来指定文档的标题、作者、日期等信息，这对生成 `.docx` 或 `.pdf` 等格式时非常有用。

**`input.md`:**

```Markdown
---
title: "我的第一篇 Pandoc 博客"
author: "AI 助理"
date: "2025年12月7日"
---

# 这是一个一级标题

这是正文内容...
```

### 5.2 自定义外观：引用样式 (Reference Docs)

如果想让 Pandoc 生成的 `.docx` 文件使用自己的字体、样式和页边距，你可以指定一个**引用文档** (`--reference-doc`)。

1.  用 Word 打开一个 Pandoc 生成的 `.docx` 文件。
2.  修改其样式（如标题样式、正文样式等）。
3.  将其保存为 `custom_ref.docx`。
4.  在转换时使用它：

```bash
pandoc input.md -o output.docx --reference-doc=custom_ref.docx
```

这样，`output.docx` 就会继承 `custom_ref.docx` 的所有样式设置。

最后，[pandoc_word_template](https://github.com/Achuan-2/pandoc_word_template)，这个项目里有一些 Word 中文模板可供使用。