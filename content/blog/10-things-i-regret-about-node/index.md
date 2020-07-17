---
title: 10 things I regret about Node - Ryan Dahl
description: NodeJS flaws exposed by creator Ryan Dahl during JSConf EU, 2018...
date: 2020-02-03
---

![](./assets/ryan-dahl.jpg)

# The Challenge:

<u>Node.js</u> is a JavaScript runtime utilized by a huge number of associations and individuals and has around **_7 million_** dynamic clients every month.

With more than **_15 million_** open source downloads every month and in excess of a **_billion_** bundle downloads every week, Node.js is viewed as the greatest computerized change stage controlling everything from web, IoT and work area applications to microservice structures.

It is the runtime of decision for elite, low idleness applications, fueling everything from big business applications, robot, API motors, cloud stacks, and portable sites.

As a very well known open source venture, Node.js battled with developing agonies. The first improvement was supported by Joyent (obtained by Samsung) and after just about three years of very quick turn of events, the undertaking had developed generously and had countless engineers downstream who were getting progressively dependent on Node.

By 2014, it was evident that Node.js was transformatively affecting the business. The stakes around Node.js were getting higher. Developing accomplishment as an open source venture and a developing biological system of sellers made a turbulent scene. This brought about many equal and frequently clashing advancement endeavors and contradictions that eased back discharges.

Notwithstanding the moderate discharges, Node.js appropriation was developing rapidly and endeavors were searching for greater security with Node.js, including plans for long haul support. While free designers were searching for quicker discharge cycles. The present condition of the venture required an alternate legislative structure.

## So, what did he regret about Node.js? Lets take a look.

### Overview

The goal was to heavily focus on programming event driven HTTP servers when he created Node and Go. Go is a language to build fast servers. But he sufficed JavaScript is nice. Dynamic languages may not suit for building a server, in which you want to control everything, but are the right tool for prototyping.

The problems with Node runtime are almost around how it manages user code mainly because he focused on the evented I/O (IOCP, epoll, kquery), the module system essentially became an afterthought.

### Introduction

Dynamic languages are great for many things, but in a server, one want things to be statically typed. He didn't stick with Promises in Node (when he introduced them in June 2009), later removed them a year after on February 2009. Keeping them could have sped up the whole process of async/await development.

The security and vulnerabilities due to GYP build system. And the last but not the least package.json or a centralized (privately controlled) repository for modules that was an unnecessary abstraction that kept record of repositories and modules that wasn’t require at all.

> _And the 10 reasons (not exactly 10 if I know how to count, well we will only talk through the top 6 uncertainties and leave apart the trivial)_

##**_1. <u>Not sticking with promises_**</u>

He added promises to Node in June 2009 but removed them in February 2010 for minimal configuration. It’s possible unified usage of promise in Node would have sped the delivery of the standardization and async/await process.

##**_2. <u>Security_**</u>

Node program can access all the system calls, such as writing to the disk, accessing to the network. This is due to build system (GYP) that he used on Node.js.

##**_3. <u>Build System_**</u>

If you are writing a module links to a C library, you’d use GYP to compile that C library and link it into Node. Chrome used GYB once, but now Node is the sole GYP user. Node has several unnecessary complex wrappers around it.

##**_4. <u>Package.json_**</u>

Including NPM in the Node making NPM the standard of the Node distribution. It is the centralized (privately controlled) repository for modules. The `require(“sommodule”)` is not specific ad install unwanted modules. The unnecessary abstraction to rise the concept of a “module” as a directory of files that includes unnecessary information, such as license and repository.

##**_5. <u>node_modules_**</u>

The module resolution algorithm is wildly complex and messes up with browser compatibilities.

##**_6. <u>index.js_**</u>

Needlessly complicated the module loading system and especially unnecessary after require supported package.json.

## Conclusion

He briefs about his new project Deno.js, a runtime for JavaScript and TypeScript based on the V8 JavaScript engine and the Rust programming language and how Deno.js will help conceal the flaws of Node.js.

By default a script should run without any network or file system write access. Users can opt in to access via flags and arbitrary native functions are not bound into V8. Typescript also allows code to grow seamlessly from quick hacks to large, in a well-structured machinery.

Simplifying the module system with no backwards compatibility with Node modules. Imports are relative or absolute URL's ONLY and must provide an extension. Remote URL's are fetched and cached indefinitely on the first load.
