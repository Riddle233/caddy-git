# caddy-git

<a href="https://github.com/greenpau/caddy-git/actions/" target="_blank"><img src="https://github.com/greenpau/caddy-git/workflows/build/badge.svg?branch=main"></a>
<a href="https://pkg.go.dev/github.com/greenpau/caddy-git" target="_blank"><img src="https://img.shields.io/badge/godoc-reference-blue.svg"></a>
<a href="https://caddy.community" target="_blank"><img src="https://img.shields.io/badge/community-forum-ff69b4.svg"></a>
<a href="https://caddyserver.com/docs/modules/git" target="_blank"><img src="https://img.shields.io/badge/caddydocs-git-green.svg"></a>

Git Plugin for [Caddy v2](https://github.com/caddyserver/caddy).

Inspired by [this comment](https://github.com/vrongmeal/caddygit/pull/5#issuecomment-1010440830).

Please ask questions either here or via LinkedIn. I am happy to help you! @greenpau

Please see other plugins:
* [caddy-auth-portal](https://github.com/greenpau/caddy-auth-portal)
* [caddy-authorize](https://github.com/greenpau/caddy-authorize)
* [caddy-trace](https://github.com/greenpau/caddy-trace)
* [caddy-systemd](https://github.com/greenpau/caddy-systemd)


<!-- begin-markdown-toc -->
## Table of Contents

* [Overview](#overview)
* [Getting Started](#getting-started)

<!-- end-markdown-toc -->

## Overview

The `caddy-git` allows updating a directory backed by a git repo.

## Getting Started

For example, the following configuration sets up a definition for `authp.github.io`
repo. The request to `authp.myfiosgateway.com/update/authp.github.io` trigger
`git pull` of the `authp.github.io` repository.

```
{
  git {
    repo authp.github.io {
      base_dir /tmp
      url https://github.com/authp/authp.github.io.git
      branch gh-pages
      depth 1
      update every 600 # 10 minutes
    }
  }
}

authp.myfiosgateway.com {
  route /update/authp.github.io {
    git update repo authp.github.io
  }
  route {
    file_server {
      root /tmp/authp.github.io
    }
  }
}
```