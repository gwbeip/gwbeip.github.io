# Wenbo Guo’s Academic Homepage

Source code for the academic homepage of Wenbo Guo (郭文博), built with Jekyll and published on GitHub Pages. [Live site](https://gwbeip.github.io/) · [中文说明](docs/README-zh.md)

## Update the site

| File or directory | What to edit |
| --- | --- |
| [`_pages/about.md`](_pages/about.md) | Biography, news, publications, projects, professional service, and contact information |
| [`_config.yml`](_config.yml) | Site title and description, author profile, external links, and optional analytics or site verification |
| [`_data/navigation.yml`](_data/navigation.yml) | Main menu labels and links |
| [`images/`](images/) | Profile image and browser icons |

## Preview locally

Install Ruby and Bundler, then run these commands from the repository root. On Windows, WSL lets you use the Linux platform listed in the repository’s lockfile. [GitHub Pages local preview guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)

```sh
bundle install
bundle exec jekyll serve
```

Open [localhost:4000](http://localhost:4000/) in your browser. Restart Jekyll after changing `_config.yml`.

## Publish with GitHub Pages

In the repository’s **Settings → Pages**, choose **Deploy from a branch**, then select `main` and `/(root)`. GitHub Pages rebuilds the site when changes are pushed to that source. [GitHub Pages publishing settings](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

If you use this repository for your own user site, name your repository `USERNAME.github.io` and set `repository` in [`_config.yml`](_config.yml) to `USERNAME/USERNAME.github.io`. Replace the author profile and homepage content before publishing.

## Update Google Scholar citations

1. Copy the value of the `user` parameter from your Google Scholar profile URL.
2. In **Settings → Secrets and variables → Actions**, add a repository secret named `GOOGLE_SCHOLAR_ID` with that value. [GitHub Actions secrets](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets#creating-secrets-for-a-repository)
3. On GitHub, open **Actions → Get Citation Data → Run workflow** and select the default branch. The workflow file needs to be on that branch for the button to appear. If you created a fork, enable its workflows in **Actions** first. [Manual workflow runs](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/manually-run-a-workflow)

The [workflow](.github/workflows/google_scholar_crawler.yaml) runs on `ubuntu-26.04` with Python 3.12. It is scheduled for Mondays at 08:00 Beijing time (`Asia/Shanghai`) and can also run on demand.

A successful run publishes `gs_data.json` (author and publication statistics) and `gs_data_shieldsio.json` (the homepage citation badge) to the [`google-scholar-stats` branch](https://github.com/gwbeip/gwbeip.github.io/tree/google-scholar-stats). Check that branch first if the badge looks stale. When `google_scholar_stats_use_cdn` is enabled, CDN caching can delay what appears on the homepage.

If a run fails, open the failed step in **Actions** to identify whether dependency installation, data fetching, or publishing failed. The [crawler requirements](google_scholar_crawler/requirements.txt) keep `bibtexparser` below 2 because the installed version of `scholarly` uses its 1.x API.

## Credits and license

The site is based on [AcadHomepage](https://github.com/RayeRen/acad-homepage.github.io), which draws on [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) and [Academic Pages](https://github.com/academicpages/academicpages.github.io). It uses [Font Awesome](https://fontawesome.com/). See the [MIT license](LICENSE) for the site code.
