---
layout: post
title:  "Notifying `systemd` that your application is ready"
tags: [systemd]
---

**TL;DR**

```
[Service]
Type=notify
NotifyAccess=all
TimeoutSec=an appropriate value for your application
```

## Problem

For whatever reason, you may want to notify `systemd` that your application is ready.

## Solution

Your service can have the `Type` defined as `notify`: Then, [it is expected that the service sends a notification message via sd_notify(3) or an equivalent call when it has finished starting up](https://www.freedesktop.org/software/systemd/man/systemd.service.html).

[`systemd-notify --ready`](https://www.man7.org/linux/man-pages/man1/systemd-notify.1.html) is a way of letting `systemd` know your app is ready. There may be a library to do this in your language, as the `sd_notify` gem for Ruby.

So, the first step is to change the `Type` of your service to `notify`.

Then, you should look at what value do you need for `NotifyAccess`. It'll depend on how you start your app. If the process configured with `ExecStart` is the main process of the service, then it should be fine with `main` or `exec` - I couldn't find in the documentation if there's a difference; it treats it as the same. However, if the command you have in `ExecStart` starts a new process that is the actual app, then your `NotifyAccess` should be `all`. Unless you start the new process with the same PID, which can be achieved by using `exec` when starting it, for example.

You should also look to how long your app takes to start. If it takes more than the default value for `TimeoutStartSec` or `TimeoutSec`, then you must update it. Otherwise, `systemd` kills your app before it's able to notify `systemd` that it's ready, then `systemd` tries to launch it again, but it will never succeed since probably it will timeout again. Then your service will be stuck in `activating` state.
