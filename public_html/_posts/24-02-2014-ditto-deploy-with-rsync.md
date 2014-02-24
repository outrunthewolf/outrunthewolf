---
layout: entry
title: Ditto, deployment with rsync
---

I use PHP too much. One of the more annoying issues we encounter is quick and simple deployment of applications. We've used many systems to orchaestrate these deployments over time, capistrano, fabric, by hand with git and composer, but they all tend to be more work than I think is neccessary.

Sometimes the old ways are the best, and one of the best of the old ways is rsync. I've overlooked it for newer more exciting systems but recently i've fallen back in love with it.

So I introduce [ditto](https://github.com/outrunthewolf/ditto "ditto: rsync for deployment") which is a simple bash wrapper around rsync. I'm hoping to keep it very light, I don't want to start small and end up building just another problem.

I have a mental roadmap for getting it perfect, and I'd love any feedback or ideas.

