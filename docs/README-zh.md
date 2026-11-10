# 郭文博的个人学术主页

本仓库保存郭文博（Wenbo Guo）个人学术主页的源码，使用 Jekyll 构建并通过 GitHub Pages 发布。 [访问主页](https://gwbeip.github.io/) · [English README](../README.md)

## 更新主页

| 文件或目录 | 修改内容 |
| --- | --- |
| [`_pages/about.md`](../_pages/about.md) | 个人简介、动态、论文、项目、学术服务和联系方式 |
| [`_config.yml`](../_config.yml) | 网站标题与描述、作者资料、外部链接，以及可选的访问统计和站点验证 |
| [`_data/navigation.yml`](../_data/navigation.yml) | 主导航的名称和链接 |
| [`images/`](../images/) | 头像和网站图标 |

## 本地预览

安装 Ruby 和 Bundler，在仓库根目录执行以下命令。Windows 用户可以通过 WSL 使用依赖锁定文件中列出的 Linux 平台。 [GitHub Pages 本地预览指南](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)

```sh
bundle install
bundle exec jekyll serve
```

在浏览器中打开 [localhost:4000](http://localhost:4000/)。修改 `_config.yml` 后需要重启 Jekyll。

## 发布到 GitHub Pages

在仓库的 **Settings → Pages** 中选择 **Deploy from a branch**，将发布来源设为 `main` 分支的 `/(root)`。推送到该分支后，GitHub Pages 会重新构建网站。 [GitHub Pages 发布设置](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

如果用本仓库搭建自己的用户主页，将仓库命名为 `USERNAME.github.io`，并将 [`_config.yml`](../_config.yml) 中的 `repository` 改成 `USERNAME/USERNAME.github.io`。发布前替换作者资料和主页内容。

## 更新 Google Scholar 引用统计

1. 从 Google Scholar 个人主页网址中复制 `user` 参数的值。
2. 在 **Settings → Secrets and variables → Actions** 中新增仓库密钥 `GOOGLE_SCHOLAR_ID`，填入刚复制的值。 [GitHub Actions 密钥设置](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets#creating-secrets-for-a-repository)
3. 在 GitHub 上打开 **Actions → Get Citation Data → Run workflow**，选择默认分支并运行。工作流文件需要位于默认分支，页面上才会出现运行按钮。若使用 fork，请先在 **Actions** 中启用工作流。 [手动运行工作流](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/manually-run-a-workflow)

[引用统计工作流](../.github/workflows/google_scholar_crawler.yaml) 使用 `ubuntu-26.04` 和 Python 3.12，每周一北京时间 08:00 定时运行，也支持手动运行。

运行成功后，`gs_data.json`（作者和论文引用数据）与 `gs_data_shieldsio.json`（首页引用徽章数据）会发布到 [`google-scholar-stats` 分支](https://github.com/gwbeip/gwbeip.github.io/tree/google-scholar-stats)。如果徽章未及时刷新，先核对该分支的文件。启用 `google_scholar_stats_use_cdn` 时，CDN 缓存可能让首页稍晚显示新数据。

如果工作流失败，在 **Actions** 中展开失败步骤，确认问题出在依赖安装、数据抓取还是发布。[爬虫依赖文件](../google_scholar_crawler/requirements.txt) 将 `bibtexparser` 限制在 2.0 以下，因为当前的 `scholarly` 仍使用它的 1.x 接口。

## 致谢与许可

网站基于 [AcadHomepage](https://github.com/RayeRen/acad-homepage.github.io)，该项目参考了 [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 和 [Academic Pages](https://github.com/academicpages/academicpages.github.io)。网站使用 [Font Awesome](https://fontawesome.com/)。站点代码采用 [MIT 许可证](../LICENSE)。
