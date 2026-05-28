# Ubuntu + VSCode + TeX Live 配置简明流程

本文记录在 Ubuntu 下配置 VSCode + TeX Live + LaTeX Workshop 的基本流程，适合用于中文 LaTeX 文档、论文、报告编写。

## 1. 安装 TeX Live

通过https://tug.org/texlive/acquire-iso.html来下载TeX Live ISO 镜像。

如果已经下载 TeX Live ISO 镜像，进入镜像挂载目录后执行：

```bash
sudo ./install-tl
```

进入安装界面后，通常直接输入：

```text
I
```

开始安装。

安装完成后，TeX Live 默认路径通常为：

```bash
/usr/local/texlive/2026/bin/x86_64-linux
```

## 2. 配置环境变量

打开 `~/.bashrc`：

```bash
nano ~/.bashrc
```

在文件末尾加入：

```bash
export PATH=/usr/local/texlive/2026/bin/x86_64-linux:$PATH
export MANPATH=/usr/local/texlive/2026/texmf-dist/doc/man:$MANPATH
export INFOPATH=/usr/local/texlive/2026/texmf-dist/doc/info:$INFOPATH
```

使配置生效：

```bash
source ~/.bashrc
```

检查是否安装成功：

```bash
which xelatex
xelatex --version

which latexmk
latexmk --version
```

如果能看到 `/usr/local/texlive/2026/bin/x86_64-linux/xelatex`，说明 TeX Live 已正确安装。

## 3. 安装 VSCode 插件

在 VSCode 扩展商店中安装：

```text
LaTeX Workshop
```

该插件用于编译 `.tex` 文件、预览 PDF、管理 BibTeX 参考文献和辅助文件。

## 4. 推荐项目结构

```text
latex-project/
├── main.tex                 # 主 tex 文件
├── refs.bib                 # 参考文献
├── README.md                # 项目说明
├── figures/                 # 图片资源
│   └── example.jpg
├── sections/                # 分章节 tex 文件，可选
│   ├── intro.tex
│   └── method.tex
├── tables/                  # 表格文件，可选
├── build/                   # 编译输出目录
├── .vscode/
│   └── settings.json        # 只针对本项目的 VSCode 配置
└── .gitignore               # Git 忽略规则
```

## 5. 总结

推荐配置逻辑：

```text
TeX Live 提供 xelatex、latexmk、bibtex
VSCode 负责编写 tex 文件
LaTeX Workshop 负责调用编译命令和预览 PDF
settings.json 负责定义编译工具、编译流程和预览方式
```

日常使用方式：

```text
打开 tex 文件 → 修改内容 → Ctrl + S → 自动编译 → PDF 预览自动刷新
```