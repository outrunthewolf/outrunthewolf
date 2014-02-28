---
layout: entry
title: Why I use Docker
---

One of the main reasons I use Docker is to liberate my working environment from dependencies.

I often find myself running multiple stacks, nginx, Apache, Jekyll etc... On top of that they all have their depencies.

When you're using a single machine you will constantly find yourself installing these dependencies and web stacks over and over, sometimes they conflict, sometimes you need different versions, and all the while if your not using Apache today, its sat around quietly wasting resources.

### How Docker helps
By using docker you can free your system from all these applications and run them whenever you truly need them.

Docker also gives you the ability to drill this down further.

Let's say I maintain a specific nginx container, I also have Zend container and a Laravel container. When i know I'll be using Zend or laravel with nginx, I simply boot a new instance of the framework contaoner, extending the base nginx container, and bobs your uncle a fully working web stack and framework independent of your local machine.

Most of these containers I'm in the middle of moving to my home server, to speed up the process and localise things more effectively.

### Start small
It takes a little time to set up, but in the long run its quick to use, very easy to update for new or even multiple versions of a particular application.

I started off by identifying my most commonly used applications, and working them into Dockerfiles, I only started with projects that weren't overly important or had tight deadlines. This
way I got used to using docker and over time built up quite a few container types.

### Final state of affairs
My laptop now only contains my personal files and my code repositories. I run PHP, Ruby, Python and Go, along with Apache, Nginx, MySQL, Mongo and Redis all within their own containers, none of those programs actually exist natively on my laptop.

I do have to boot a container each time I want to use them, but it takes little to no effort, and once my application is done, I can package the whole thing up within a docker container, and run it wherever I like, without having to worry about missing dependencies.
