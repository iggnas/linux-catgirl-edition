# The Linux Catgirl Edition kernel

Striving to offer the best possible desktop and server Linux experience, in a novel way.

## Novel way?

yeah. most if not all of those custom kernels are conservative with their changes, in order to essentally make it a drop-in kernel. Nothing wrong with that.

but linux-catgirl-edition, on the other hand, doesn't hold back. We make certain assumptions about the user and disable certain core linux features, as we assume
it does not affect the end user.

want an example? linux-zen has module unloading support. when was the last time you ran `modprobe -r --remove-holders i915`? probably never.

## Principles

### You are a gamer.

catgirl edition offers the option to disable debugging features because lets be real, you are never going to run gdb to read `/dev/kcore`, run `perf`, or `samply`, right after a gaming session.

bet you never knew those were a thing.

### You are a server.

catgirl edition offers the option to disable debugging features because lets be real, you are never going to run gdb to read `/dev/kcore`, run `perf`, or `samply`, in production.

bet you never knew those were a thing.

### You don't run VMs.

catgirl edition makes the assumption that:

1. the kernel will not run in a vm
1. the kernel will not run any vms

this allows us to disable things like XEN drivers, a paravirtualization layer, remove certain virtualization drivers.

### You are not [somebody that's under investigation by law enforcement].

catgirl edition offers the option to disable various security features for performance. Some ranging from runtime checks like
KASAN* or actual security features like SELINUX.

> [!WARNING]
> it being an option does not imply that you should. explore your threat model carefully.

## Why only cachyos patchset?

too lazy to make sure clearlinux and xanmod patches all work, so cachyos patchset until i have more time on my hands.

---

## Where can I get linux-catgirl-edition?

You can download the precompiled package either from the [releases page](https://github.com/pparaxan/linux-catgirl-edition/releases) or build from the [actions page](https://github.com/pparaxan/linux-catgirl-edition/actions).

## How do I compile linux-catgirl-edition locally?
* Make a folder named "linux-catgirl-edition" and place the [PKGBUILD](https://github.com/pparaxan/linux-catgirl-edition/blob/main/PKGBUILD) inside it.
* Run the command `makepkg -scf --cleanbuild --skipchecksums` to install the package.

That's it, Enjoy the Catgirl Edition of Linux!
