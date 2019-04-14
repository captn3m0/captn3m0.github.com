---
title: Stripping Audible DRM
layout: post
tags:
    - DRM
    - audible
---

Self-Guide for stripping the Audible DRM, in similar vain as my [Kindle Self-Guide](/blog/2019/03/26/kindle-self-guide/).

1. Download the aax file from Audible website.
2. Run the inAudible-NG Rainbrow crack table against the AAX file.

Easiest way is via docker:

```
cd ~/Music/Audiobooks
docker run -v $(pwd):/data ryanfb/inaudible
```

The cool part about this is that the entire activation is done offline, and runs a Rainbow Table attack against the Audible DRM.

The docker image checksum is `sha256:2f8dd34cdc3c97e85b0acfe98cb777df2db6046d0c796ae6ec982af95c51aae1` as of my last use.

## References

- <https://github.com/ryanfb/docker_inaudible_rainbowcrack>
- <https://github.com/inAudible-NG/tables>
