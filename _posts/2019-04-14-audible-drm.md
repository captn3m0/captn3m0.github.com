---
title: Stripping Audible DRM
layout: post
tags:
    - DRM
    - audible
---

Self-Guide for stripping the Audible DRM, in similar vein as my [Kindle Self-Guide](/blog/2019/03/26/kindle-self-guide/).

1. Download the aax file from Audible website.
2. Run the inAudible-NG Rainbrow crack table against the AAX file.

Easiest way is via docker:

```
cd ~/Music/Audiobooks
docker run -v $(pwd):/data ryanfb/inaudible@sha256:b66738d235be1007797e3a0a0ead115fa227e81e2ab5b7befb97d43f7712fac5
```

The cool part about this is that the entire activation is done offline, and runs a Rainbow Table attack against the Audible DRM.

## References

-   <https://github.com/ryanfb/docker_inaudible_rainbowcrack>
-   <https://github.com/inAudible-NG/tables>
