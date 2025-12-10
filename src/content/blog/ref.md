---
title: Zotero 导出 GB/T 7714-2015 参考文献格式
description: 拒绝手搓参考文献，一文搞定 Zotero 国标格式安装与三种导出姿势，包含解决“et al”混排问题的核心思路。
publishDate: 2025-12-10
---

最让人头大的不是写 Introduction，而是最后那个该死的参考文献列表。作为一个 CS 人，手动调整 [1]、[2] 和逗号句号是绝对不能接受的。

下文把 Zotero 调整为 GB/T 7714-2015（国标 2015）格式的流程整理了一下，以此备忘。

## 1. 环境配置

Zotero 默认只有 APA、IEEE 等国外常见格式，国内高校要求的 GB/T 7714 需要手动添加。

1.  **进入设置**：
    -   Windows: `编辑 (Edit)` -> `首选项 (Settings)`
    -   Mac: `Zotero` -> `设置 (Settings)`（`Command+,`）
2.  **加载样式库**：
    -   点 `引用 (Cite)` -> `样式 (Styles)` 标签页。
    -   点击下方不起眼的文字链接：`获取更多样式... (Get additional styles...)`。
3.  **搜索并安装**：
    -   搜索框输入 `GB/T`。
    -   CS 论文一般用顺序编码制，所以认准这个：**China National Standard GB/T 7714-2015 (numeric)**。
    -   点击它，安装国标样式。

## 2. 导出参考文献

### A. Word/WPS

这是最稳的方案，利用 Word 插件实现“引用处自动标号 + 文末自动生成列表”。

1.  Word 顶部菜单栏找 `Zotero`。
2.  点 `Document Preferences`，样式选刚才装好的 `China National Standard GB/T 7714-2015 (numeric)`。
3.  光标放在需要插入引用的地方，点 `Add/Edit Citation`。
4.  最后在文末点 `Add/Edit Bibliography`，列表自动生成。
    -   *优势：文中删改段落，序号会自动更新，不用人工维护。*

### B. 临时需要

不需要联动，只需要纯文本。

1.  在 Zotero 列表里按住 `Ctrl/Cmd` 选中要用的那几篇文献。
2.  右键 -> `由所选条目创建参考文献表 (Create Bibliography from Items...)`。
3.  配置：
    -   **样式**：选 GB/T 7714-2015。
    -   **输出方法**：选 `复制到剪贴板 (Copy to Clipboard)`。
4.   `Ctrl+V` 即可。

### C. 导出文件分享给导师

如果导师要检查文献库。

1.  右键点击左侧的 Collection（分类文件夹）。
2.  `导出分类 (Export Collection)`。
3.  格式选 `Bibliography` -> 样式选 GB/T 7714-2015。
4.  导出为 RTF 或 HTML 文件。

## 3. 避坑指南

配置好后可能会遇到一个经典 Bug：中英文混排时的“et al”和“等”不分。

比如中文文献后面跟着个 "et al"，或者英文文献后面冒出来个 "等"。

-   **原因**：Zotero 原生逻辑对语言判定较弱。
-   **解决方案**：不要试图手动改元数据！去 Github 或者插件市场下个 **Jasminum（茉莉花）** 插件。
    -   这插件专门治各种不服的中文元数据，装好后重启 Zotero，不仅能自动识别中英文调整“等/et al”，还能抓取知网数据。