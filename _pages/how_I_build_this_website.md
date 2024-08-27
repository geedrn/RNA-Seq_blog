---
title: How I built this website
author: Ryo Niwa
date: 2024-08-22
category: Website
layout: post
---

This website is powered by [jekyll-gitbook](https://github.com/sighingnow/jekyll-gitbook).
I simply forked the repository from the github and pasted them into my own repo. 

I use docker-ed jekyll for local procedures,. Here is my typicall command for a quick check after updating markdown.

```bash=
docker run --rm \
  --volume="$PWD:/srv/jekyll:Z" \
  --publish 127.0.0.1:4000:4000 \
  -it jekyll/jekyll:4.2.0 \
  sh -c "bundle install && jekyll serve"
```

I used remote theme function supported on Github pages. See details from the [link](https://sighingnow.github.io/jekyll-gitbook/jekyll/2019-04-28-howto.html). 

jekyll-gitbook is open sourced under the Apache License, Version 2.0, using the same license as the original GitBook repository.