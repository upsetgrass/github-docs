# github_action

workflows中的yml是自动构建工具，和makefile mill等工具类似，只不过worflows是github中action组件自动执行的，这一部分用于创建分支gh-pages，单独存储mdbook build构建出来的那些html还有一些依赖文件，以保持其他分支的洁净，并设定自动更新文档的条件，具体示例如下，基本可以直接使用

```yaml
name: deploy-github-pages  # 定义workflow或步骤名称
on:                        # on:触发条件
  push:
    branches:
      - main               # 当main分支有新的push，触发该github action
jobs:
  deploy-github-pages:     # 使用最新的Ubuntu作为执行环境
    runs-on: ubuntu-latest # 运行环境
    permissions:           # 设置权限，使得action可以向gh-pages分支写入
      contents: write
    steps:                 # 以下都是各个任务
      - name: Checkout repository         # 步骤名称
        uses: actions/checkout@v4  # uses-使用github action中写好的脚本，这里是在拉取我的代码

      - name: Setup mdBook
        if: ${{ github.ref == 'refs/heads/main' }}
        uses: peaceiris/actions-mdbook@v1.2.0       # 主分支上安装mdbook
        with:
          mdbook-version: '0.4.5'

      - name: Build site
        if: ${{ github.ref == 'refs/heads/main' }}
        working-directory: .
        run: mdbook build                           # 主分支上运行mdbook build指令

      - name: Move HTML files to root 
        run: |                                      # run: | 运行多行shell脚本
          mv ./book/html/* ./book/
          rm -r ./book/html

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3  # 使用该actions用于自动部署github pages
        if: ${{ github.ref == 'refs/heads/main' }}
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./book               # 指令主分支的./book内容作为gh-pages分支的内容
          force_orphan: true                   # 删除gh-pages的历史记录  ，只保留最新版本
```
本质：workflows中的操作就是github帮我们在某种触发下，自动执行某些指令。比如上面就是push到主分支时，执行后面的操作，后面的操作就是github把我们的主分支的代码pull下来，然后下载mdbook执行mdbook build，然后创建gh-pages分支，将生成的/book推送到我的仓库的gh-pages分支上。