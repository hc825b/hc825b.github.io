# hc825b.github.io

Chiao's Personal Website

This is the project to develop Chiao, the view of myself as a computer
scientist and a researcher.


## Develop locally

### Install Ruby and Bundler

I use the command below on Ubuntu 20.04.

```bash
$ sudo apt install ruby-dev ruby-bundler
```

### Install dependencies without sudo access

```bash
$ bundle config set --local path 'vendor/bundle'
$ bundle install
```

### Build website locally with bundle

Add `--host=0.0.0.0` to allow all accesses to Window Subsystem for Linux.

```bash
$ bundle exec jekyll serve --incremental --host=0.0.0.0 --port 8000
```
