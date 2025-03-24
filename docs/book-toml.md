# book.toml
```toml
[book]
authors = ["upsetgrass"]
language = "zh"
multilingual = false
src = "docs/"
title = "note_test"

[output.html]
git-repository-url = "https://upsetgrass.github.io/note/"
mathjax-support = true

[output.pdf]
optional = true
```
这是一个示例，有三个部分book、output.html、output.pdf
[\book] - 用于设置书籍，作者是upsetgrass，该文档的语言是中文，不支持多语言，src源文件目录，所有的markdown章节都放在docs目录下，书籍的标题是note_test，显示在index.html页面的 <\title> 标签中
[\output.html] - 配置 mdBook 生成 HTML 格式文档的参数，git-repository-url，会在生成的 HTML 文档的右上角添加一个指向该 Git 仓库的链接，mathjax-support用于是否启用MathJax公式支持，Makrdown中使用LateX数学公式
对于每一个md生成的html会生成在本地的book路径下