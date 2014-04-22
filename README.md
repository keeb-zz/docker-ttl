# docker-ttl

Container time-to-live - stop a container if it has been running too long.

# Usage

An oh-so-simple command will get you started:

```docker run -v /usr/bin/docker:/bin/docker -v /run/docker.sock:/run/docker.sock keeb/docker-ttl <ttl> <image> <image opts>```

i.e

 ```docker run -v /usr/bin/docker:/bin/docker -v /run/docker.sock:/run/docker.sock keeb/docker-ttl 10s busybox sh -c 'echo hello && sleep 30'```

# Wat

Ever wanted to make sure that a container lives no more than X amount of time? I sure have, hence this.

# Why this way?

There are a few ways of accomplishing the same goal, from stupid simple to incredibly robust. They include:

* Just running the script on the host
* Creating some sort of event dispatch / subscription based on `docker events`
* If you need ttl containers, baking this functionality in to the app which spawns them
* Arguably, should be in the docker API - see https://github.com/dotcloud/docker/issues/1905

So, why this way?

My goal is to Dockerize All The Things! As a result, option 1 is a non starter. Running anything but containers on the host means I'm not trying hard enough. Sure, that's dogmatic. So what?

An event dispatch / toolkit of some sort would be great, but that is way more than I need for right now. I do love the idea of utility containers; especially something which can react to events of a Docker-based cluster. Hmm!

Actually, this model mostly follows the *core tenets of the plugin model Docker*. What's a plugin? A container, silly! Why would it be anything else? 

Granted, it's a special container which has access to the Docker daemon, which means it can do anything a host can do. The plugin model will make this seamless, and also introduce the idea of scoped operations, so you do not have wanton processes doing whatever the hell they want.


