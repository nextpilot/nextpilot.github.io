# Nextpilot Project Website

 当前仓库存储了 nextpilot 项目网站源代码，基于 [MKDocs](https://www.mkdocs.org/) + Markdown 构建，并使用 [mkdocs-material](https://squidfunk.github.io/mkdocs-material/) 主题。 当推送 main 分支时，会自动激活 [github action](.github/workflows/build-page-docs.yml) 进行文档编译，并发布到 [gh-pages](https://github.com/nextpilot/nextpilot.github.io/tree/gh-pages) 分支。

## 访问网站

您可以通过 <https://nextpilot.cn> 或 <https://nextpilot.github.io> 访问 nextpilot 项目网站。

## 编译文档

您可以通过以下方式编译项目：

```shell
# 安装pip依赖项
pip install -r requirements.txt

# 编译文档
mkdocs build

# 本地服务
mkdocs serve
```
