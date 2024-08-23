---
title: How I build this website
author: Ryo Niwa
date: 2024-08-22
category: Website
layout: post
---

This website is powered by jekyll-gitbook [https://github.com/sighingnow/jekyll-gitbook].
I simply forked the repository from the github and pasted them into my own repo. 

For local procedures, I use docker-ed jekyll. Here is my typicall command for a quick check after updating markdown.

```bash=
JEKYLL_VERSION=4.2.0 docker run --rm \
  --volume="$PWD:/srv/jekyll:Z" \
  --publish 127.0.0.1:4000:4000 \
  -it jekyll/jekyll:$JEKYLL_VERSION \
  sh -c "cd /srv/jekyll/rna-seq && bundle install && jekyll serve"
```

