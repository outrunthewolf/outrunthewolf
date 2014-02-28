---
layout: entry
title: Vagrant cannot forward the specified ports on this VM
---

I use vagrant on mac for Docker. When Vagrant boots it opens up all ports between 4000 and 5000 which are the random ports Docker uses to forward to its local connections.

When I ran Vagrant for the first time after installing an OSX patch I kept getting this error:

![Vagrant Port Error]({{}}/images/vagrant-port-error.png)

At first I thought there was a left over VM still running, so I looked for an instance of Virtual Box.

```sh
$ ps -ef | grep VBox
```

Nothing. So I then checked what programs were listening on what port.

```sh
$ lsof -i | grep LISTEN
```

Interestingly it turned out that Steam (the game client) and AeroFS (a backup program) were both utilising some of Dockers ports.
Closing Steam and AeroFS fixed the issue, but I never knew they utilised those ports. Something to keep in mind.
