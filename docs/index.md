# 项目文档结构
```
├──.github/workflows/dbook.yml
├── book.toml
├── src/
│   ├── SUMMARY.md  # 目录结构定义
│   ├── index.md
│   ├── chapter_1.md
│   ├── chapter_2.md
│   ├── images/
│   │   ├── example.png
│   ├── theme/
│   │   ├── custom.css
├── book/
```
简要说明：  

1、book.toml中是用于设置文档/书籍、输出形式的相关设置  

2、src子目录下存放源文件，包括源文档（.md），静态资源（images目录下）、模板文件（theme目录下），其中必须有一个SUMMARY.md文档，用于存储文档的目录结构，必须有一个index.md，用于指定进入页  

3、.github/workflows/dbook.yml用于github进行action自动化进程，用于检查、解决打开生成的html文档时的一些问题  

4、book是文档生成的一些结果信息  

5、整个项目利用mdbook进行，mdbook的下载需要Rust编译环境，流程如下  
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`  
这一步时会询问下载方式一般选择-立即安装Rust、Cargo-直接点Enter  
此时rust会安装到~/.cargo/bin/ 此时还需要手动加入到PATH  
`export PATH="$HOME/.cargo/bin:$PATH" >> ~/.bashrc `  
`source ~/.bashrc`  
此时就可以用cargo工具安装mdbook，需要注意，cargo指令是用户级管理，不要用sudo  
`cargo install mdbook`  
`cargo install mdbook-pdf`  