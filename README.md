# hc825b.github.io

Chiao's Personal Website

This is the project to develop Chiao, the view of myself as a computer
scientist and a researcher.


## Develop locally

### Install dependencies without sudo access

```bash
bundle install --path vendor/bundle
```

### Build website locally with bundle

Add `--host=0.0.0.0` to allow all accesses to Window Subsystem for Linux.

```bash
$ bundle exec jekyll serve --incremental --host=0.0.0.0 --port 8000
```
