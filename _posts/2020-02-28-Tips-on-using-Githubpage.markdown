---
layout: post
title:  "Tips on combing Jekyll and Github page"
date:   2020-02-28 15:27:52 -0800
categories: Coding Tips
---

After two days study, I finally built my blog website on GitHub using Jekyll.
Of course, I have encountered some questions in practical operation and spent quite some time to solve them.
Here are some resources and tips.

## A tutorial I following:
[Building a static website with Jekyll and GitHub Pages](https://programminghistorian.org/en/lessons/building-static-sites-with-jekyll-github-pages)

It is quite detailed and you can just follow it from installing to publishing.

## Some useful website:
1. [Jekyll Talk forum](https://talk.jekyllrb.com/)You can find solutions to most of your questions.
2. [jekyllrb.com](https://jekyllrb.com/)The official website.

## Problem in installation:

The Jekyll is based on `ruby`. Since I am using MacOS, it has embedded ruby program.
When I used `brew` to install new version ruby, the system will only link to the old embedded version.
And it's complicated to upgrade that old one and then link to Jekyll, here is the solusion:

<pre><code>
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
</code></pre>

## Publishing by GitHub Pages:

1. No style and posts on webpage:[(reference)](https://talk.jekyllrb.com/t/github-pages-docs-posts-cannot-be-reached/1144)
Different from localhost, GitHub Pages need `baseurl`, in my case it should be `/blog` in
<span style="color: red">"https://shunyang2018.github.io/blog/"</span>
2. No image in posts:[(reference)](https://talk.jekyllrb.com/t/i-cannot-get-an-image-to-display/850)
Still, need basefurl when citing images: `/blog/image/`















