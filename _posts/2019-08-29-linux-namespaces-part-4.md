---
layout: post
title: "An Example Post"
categories: posts
excerpt: "Explaining Linux Namespaces"
tags: [linux, namespaces, docker, container]
comments: true
share: true
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

## The ip Command ######

> Since we will be interacting with network devices in this post, we will re-enforce the superuser requirements that we relaxed in the previous posts. From now on, we will 

{% highlight bash %}
$ ip link list
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:96:2e:3b brd ff:ff:ff:ff:ff:ff
{% endhighlight %}


Star of the show here is the `ip` command - the [Swiss Army Knife](https://access.redhat.com/sites/default/files/attachments/rh_ip_command_cheatsheet_1214_jcs_print.pdf){:target="_blank"} for networking in Linux - and we will use it extensively in this post.
Right now we have just run the `link list` subcommand to show us what networking devices are currently available in the system (here we have `lo`, the loopback interface and `ens33` an ethernet LAN interface).
\\
\\
As with all other namespaces, the system starts with an initial network namespace within to which all processes belong unless specified otherwise. Running this `ip link list` command as-is gives us the networking devices owned by the initial namespace (since our shell and the `ip` command belong to this namespace).


## Named Network Namespaces ######

Let's create a new network namespace:

{% highlight bash %}
$ ip netns add coke
$ ip netns list
coke
{% endhighlight %}

Again, we've used the `ip` command. Its `netns` subcommand allows us to play with network namespaces - for example we can create new network namespaces using the `add` subcommand of `netns` and use `list` to, well, list them.
% endhighlight %}
