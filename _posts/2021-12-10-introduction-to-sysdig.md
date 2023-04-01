---
title: ":lock: Getting Started With Sysdig"
layout: post
date: 2023-02-20 22:10
tag: [Sysdig, Quickstart Guide, Cloud Security]
#image: https://sergiokopplin.github.io/indigo/assets/images/jekyll-logo-light-solid.png
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "This how-to guide was created for students at Thinkful in order to set up and use the API platform tool Postman."
category: project
author: jimmiegonzalez
externalLink: false
---

![Sysdig-Logo](/assets/sysdig.png "Sysdig Logo")

# Introduction

Sysdig is a powerful open-source monitoring and troubleshooting tool that provides system-level visibility into Linux systems. Here's a quick start guide to help you get started with Sysdig:

# Install Sysdig

You can install Sysdig on Linux by following the instructions on the official website or by using the package manager of your distribution. For example, if you are using Ubuntu, you can run the command:

```shell
# Ubuntu example
sudo apt-get install Sysdig
```

# Start Sysdig

Once you have installed Sysdig, start it by opening the terminal and running the command:

```shell
# Ubuntu example
sudo sysdig
```

# Use Sysdig

Sysdig can capture system calls, events, and metrics in real-time or from a trace file. For example, to monitor the CPU usage of a specific process, you can run the command `sudo sysdig -pc -c topcontainers_cpu`. This will display the top CPU consuming containers.

Use the `sysdig -l` command to list the available filters, and the `sysdig -c` command to list the available chisels. For example, to list the top system calls, you can run the command `sudo sysdig -l | grep -i syscall`.

You can also use Sysdig to monitor containerized environments using the `sysdig -pc` command. For example, to monitor the disk I/O of a specific container, you can run the command `sudo sysdig -pc -c topcontainers_io`.

```shell
# Monitor CPU usage of a specific process
sudo sysdig -pc -c topcontainers_cpu

# List available filters
sudo sysdig -l | grep -i syscall

# Monitor disk I/O of a specific container
sudo sysdig -pc -c topcontainers_io
```

# Analyze Sysdig Output

Sysdig generates a lot of data, so you need to know how to filter and analyze the output. For example, to filter the output by process name, you can run the command `sudo sysdig proc.name=nginx`.

Use the `-p` option to select the fields you want to see in the output, and use the `-s` option to sort the output. For example, to display the process name, PID, and CPU usage sorted by CPU usage, you can run the command `sudo sysdig -p "%proc.name %proc.pid %cpu" -c topprocs_cpu -s %cpu"`.

You can also use chisels to filter and analyze the output. For example, to display the top network connections by source IP address, you can run the command `sudo sysdig -c topconns -r tracefile.scap -k source.ip`.

```shell
# Filter output by process name
sudo sysdig proc.name=nginx

# Display process name, PID, and CPU usage sorted by CPU usage
sudo sysdig -p "%proc.name %proc.pid %cpu" -c topprocs_cpu -s %cpu

# Display top network connections by source IP address
sudo sysdig -c topconns -r tracefile.scap -k source.ip
```

# Customize Sysdig

Sysdig is highly customizable, and you can create your own filters and chisels to analyze the system behavior that you're interested in. For example, to create a custom filter that matches the network traffic of a specific process, you can run the command `sudo sysdig -A -w mychisel.lua "evt.type=connect and proc.name=myprocess"`.

Use the `sysdig -A` command to generate a list of all available fields, and use the `sysdig -C` command to create a custom chisel. For example, to create a custom chisel that displays the disk I/O of a specific process, you can create a file called `mychisel.lua` with the following content:

```shell
# Create custom filter that matches network traffic of a specific process
sudo sysdig -A -w mychisel.lua "evt.type=connect and proc.name=myprocess"

# Generate list of all available fields
sudo sysdig -A

# Create custom chisel that displays disk I/O of a specific process
function mychisel()
    local disk_io = chisel.request_field("evt.arg.data.fd_name")
    chisel.set_filter("proc.name = 'myprocess'")
    chisel.select(disk_io)
    return true
end

sudo sysdig -c mychisel
```

That's it! With these simple steps and examples, you can start using Sysdig to explore and troubleshoot your Linux system.
