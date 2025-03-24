# mdbook指令

mdbook init：对mdbook所需要的book.toml  book/ .gitignore src/ SUMMARY.md进行简单设置，也可以自行mkdir touch
mdbook build：读取book.toml配置文件，解析 src/SUMMARY.md 生成目录结构；将 src/ 目录中的 .md 文件转换为 HTML（默认存放在 book/）；复制 theme/、static/ 目录的内容到 book/。
mdbook serve -p 3000：运行一个本地的http服务器，默认为http://127.0.0.1:3000，-p可以指定为3000还是4000...，用于本地展示生成的书籍