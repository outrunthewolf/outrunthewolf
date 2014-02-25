---
layout: entry
title: 6 months with Docker, some advice
---

I've been using docker on Linux and Mac for 6 months now and my experiences have ranged from joy to deep, sobbing in the dark, frustration. Like any technology, you have to learn how to use it properly to get the best from it. I'm going to try and outline my biggest stumbling block with docker and some simple advice on moving past them nd using it succesfully.

### Mount Hell
A very early mistake was combining files and configurations within the container itself. For example, I would build my nginx configs into the dockerfile with add straight off. As soon as I found a problem with my virtual hosts, or wanted to extend them, I would have to run the entire build sequence again.
Consider your application carefully, mount your files and configurations to the container, and maintain their relative and locations with your dockerfile, this gives you the ability to change data on your local system easily affecting your containers immediately.

### The Endless Build
One of my biggest mistakes was to place too much emphasis on the docker file. My routine would be to create the perfect dockerfile, build it and run it demonised immediately. This lead to endless headaches. Sometimes my nginx configurations would fail, php-fpm wouldn't start, mysql would consistently throw errors, or my mount points would be wrong.

The key I found was to use the dockerfile to scaffold my application, then run it interactively. Once I knew things were working correctly I would commit my container, maintaining version tags, and then update my dockerfile for use again later.

### Lack Of Isolation
Dockers major benefit is being able to isolate services separately, in fact its one of the whole points of docker.
If your running a stack with docker split it up into its subsidiaries, for example a container that runs Apache and one that handles MYSQL. Then link these container to each other. That way if you ever need an nginx container with MYSQL its trivial to attach new instances of them.

### Documentation
Read the docs. Especially with regards to dockers CLI. Too often did I miss a trick, or want for something that I thought didn't exist. 
Docker is still very new, and really cool things are happening all the time. Docker has some very helpful documentation, and its really quick to get a good understanding of what is possible, so keep your finger in the pulse and check up on it regularly.

### Know When You're Beaten
Docker might seem a panacea to many solutions, but it isnt. Know when you should and shouldn't use it.
Its always exciting to introduce something new, and too many times i've gone blustering in advocating its possibilities against the practicalities.

### Seriously, Build From Source
Because its still new, things are still changing and aptitude or brew or whatever can sometimes be a bit hissy and not keep you as updated as you like.
Build it from source, its good practice, you can update regularly without hassle, and you might want to build it with certain parameters you wouldn't normally have the option to use.

### ASK!
Dockers community like many are super friendly, if you're stuck ask. The have a very active IRC channel I regularly use, and when you ask enough questions you often find yourself being able to help out other people, which feels great!