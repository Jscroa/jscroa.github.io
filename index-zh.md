---
#
# Here you can change the text shown in the Home page before the Latest Posts section.
#
# Edit jekyll-theme-simple-blog's home layout in _layouts instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#
layout: home
permalink: /index.html
header:
  image: /assets/img/home-header.jpg
tagline: > # this means to ignore newlines until "repository:"
  日常开发笔记
excerpt: >
  Write an awesome description for your new site here. You can edit this
  line in index.md. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
# repository:
#   is_project_page: false
#   show_downloads: false
#   repository_url: https://gitlab.com/lorepirri/jekyll-theme-simple-blog
#   zip_url: https://gitlab.com/lorepirri/jekyll-theme-simple-blog/repository/master/archive.zip
#   tar_url: https://gitlab.com/lorepirri/jekyll-theme-simple-blog/repository/master/archive.tar.gz
ref: home
lang: zh
---

<h2>最新文章</h2>
<div>&nbsp;</div>
{% include list-category-posts.html lang=page.lang category="articles" %}

---

<h2>最新项目</h2>
<div>&nbsp;</div>
{% include list-category-posts.html lang=page.lang category="projects" max=3 %}
