January 2021
============

Tech
----

### The Open Society and its Media

[Article](http://www.caplet.com/papers/open-media.html)

- Succeed by not doing worse: don't ask how things could be better, demonstrate how things could be worse
- "In closed societies, when arguments cannot be spoken, hard truths cannot be figured out. When people cannot openly criticize, cannot openly defend against criticism, or cannot openly propose ideas that conflict with the official truths, then they are left with mistrust and cynicism as their only defense."
- "In looking at the dangers, I saw that none of us individually is clever enough to figure out how to solve those problems. The only hope that I saw in 1988--1 no longer believe it is the only hope--is that by creating better media for the process of societal discourse and societal decision-making, we stand a much better chance of surviving the dangers posed by new technologies, so that we may live to enjoy their benefits."

### Graphics

[Video (physics of lighting)](https://www.youtube.com/watch?v=P6UKhR0T6cs&loop=0)

[Playlist (ray tracing)](https://www.youtube.com/playlist?list=PL5B692fm6--sgm8Uiava0IIvUojjFOCSR)

[Playlist (computer graphics)](https://www.youtube.com/playlist?list=PLzH6n4zXuckrPkEUK5iMQrQyvj9Z6WCrm)

- Everything is a triangle: simplest bi-planar (flat) representation
- 3d object files are just a collection of vertices (e.g. `v 101`) and faces (e.g. `f abc`)
- Scale, translation, and rotations can be applied via a single matrix operation to vertices to transform them
- Viewport changes are also just a matrix transform to adjust the vertex representations "on-screen"
- Rasterization "paints" the 3d object into a 2d presentation, checking which pixels should be coloured with which colour given the 3d scene
- Visibility problem is now generally brute-forced via large memory buffers (z-buffers), where each vertex has an encoded depth value
- Lighting can be approximated via the z-buffer as well, checking for what the light source can see (and repeating for each light source)
- Ray tracing is the "ideal" 1:1 representation of how real physics for lighting work, but only at the limit
- Denoising "blends" a sampled approximation (e.g. 5 ray samples per pixel) into a complete image
- Ray tracing has advanced extremely quickly in recent years due to enhancements in special purpose hardware (extreme memory and optimized integrated circuits for BVH traversal) but also large improvements in denoising from deep learning


Life
----

### 100 Tips For A Better Life

[Article](https://ideopunk.com/2020/12/22/100-tips-for-a-better-life/)

### 100 Ways To Live Better

[Article](https://www.lesswrong.com/posts/HJeD6XbMGEfcrx3mD/100-ways-to-live-better)
