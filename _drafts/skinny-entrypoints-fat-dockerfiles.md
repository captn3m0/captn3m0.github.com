---
layout: post
title: Skinny Entrypoints, Fat Dockerfiles
---

As I've spent more and more time writing (and maintaining) lots of
Dockerfiles for lots of different projects, I've seen a recurring
pattern of entrypoints getting complex over time.

**This is a call to arms against complicated entrypoints.**

## Exhibit 1

```bash
update_commit(){
  if [[ -n "${GIT_COMMIT_HASH-}" ]]; then
    echo "GIT_COMMIT_HASH=${GIT_COMMIT_HASH}" >> /app/.env.vault
    echo "${GIT_COMMIT_HASH}" > /app/public/commit.txt
  fi
}
```

Could be easily handled in Dockerfile:

```Dockerfile
echo ${GIT_COMMIT_HASH} > /app/public/commit.txt
```
