---
layout: post
title: Skinny Entrypoints, Fat Dockerfiles
---

As I've spent more and more time writing (and maintaining) lots of
Dockerfiles for lots of different projects, I've seen a recurring
pattern of entrypoints getting complex over time.

**This is a call to arms against complicated entrypoints.**

## Example

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

## Why

A fat dockerfile moves your complexity to the build step. Since Docker supports `RUN` during builds, this can be as complex as you wish. However, moving this to the entrypoint does the following:

1.  Your application boot times are slower
2.  Your application boots are more complicated
3.  Your application boot is dependent on the environment it is running in

The third is a very common consequence of letting complexity creep into the entrypoint. Common examples would be modifying nginx configuration before boot, or adding a few configuration flags.

A thin entrypoint moves all your complexity to the build step, ensuring that your application behaves consistently in all environments (or atleast the boot part of it does).
