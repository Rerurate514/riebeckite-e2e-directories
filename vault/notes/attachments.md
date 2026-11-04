---
publish: true
title: Images and attachments
tags:
  - sample
  - media
---

# Images and attachments

## Image

The same image is embedded twice: once with a WikiLink embed and once with a Markdown image link.

![[diagram.svg]]

![Layout diagram](/assets/diagram.svg)

## Attachment

Download the sample text file:

- [sample.txt](/assets/sample.txt)

`sample.txt` is stored in `site/public/assets/`, so Vite copies it into the build without going through the content pipeline.

## Where the files live

The image is in `vault/assets/`; the downloadable text file is in `site/public/assets/`.

Back to [[welcome]].
