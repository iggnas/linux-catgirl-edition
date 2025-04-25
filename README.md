# The Linux Catgirl Edition kernel

Striving to offer the best possible desktop and server Linux experience, in a novel way.

## Novel way?

yeah. most if not all of those custom kernels are conservative with their changes, in order to essentally make it a drop-in kernel. Nothing wrong with that.

but linux-catgirl-edition, on the other hand, doesn't hold back. We make certain assumptions about the user and disable certain core linux features, as we assume
it does not affect the end user.

want an example? linux-zen has module unloading support. when was the last time you ran `modprobe -r --remove-holders i915`? probably never.

<details>
<summary>Optimizations</summary>

note that not all optimizations are enabled by default.

## perf:

- Guess unwinder. It has zero runtime overhead as opposed to ORC and frame pointer unwinders;
- 1000Hz (techinically reduces perf [throughput] in favor of responsiveness);
- Tickless idle, because full tickless is bad[^1];
- Removed paravirtualized layer in favor of performance. However, this is negative if you try to run the kernel under a VM;
- TCP BBR3;
- No memory zero-init (!). If you don't trust your userspace apps, THEN DONT RUN THEM;
- No structure corruption checking (!);
- x86-64-v3 optimized (kernel does not do x86-64-v4);
- Performance governor by default;
- CachyOS kernel patches;
- `-O3` optimization (!);
- Uses lazy preemption by default as opposed to full preemption to balance throughput & latency (full prioritises latency, and you lose a bit of throughput);
- No module unloading. The docs say that it makes the kernel simpler and run faster;
- modify_ldt removed for lower context switch latency

## size:

- BUG() support removed;
- Removed radio drivers;
- Coredump support removed;
- Tracing infrastructure removed;
- Removed support for processors that are not Intel or AMD;
- NUMA removed, probably. I have no idea if linux enabled it again during compile and frankly im not fighting the makefile lmao;
- No module decompression in kernel. This also reduces the attack surface, but if you don't trust your userspace apps, THEN DONT RUN THEM;
- 32 bit and 16 bit support _can_ be removed

## size & perf:

- Clang ThinLTO;
- Clang;
- No prink() support. This reduces size (no more strings) and reduces overhead where printk() calls are plenty (eg during boot, resume);
- Scheduler debugging removed;
- Trim unused headers to help LTO and optimization if headers are disabled

... aaaand much more (probably).

[^1]: source: i made it up.

</details>

---

## Where can I get linux-catgirl-edition?

You can download the precompiled package either from the [releases page](https://github.com/pparaxan/linux-catgirl-edition/releases) or build from the [actions page](https://github.com/pparaxan/linux-catgirl-edition/actions).

## How do I compile linux-catgirl-edition locally?

* Clone this repository, and **c**hange **d**directory into it.
* This is important, open the `PKGBUILD` file and enable or disable any optimizations you may or may not want[^2].
* Run the command `makepkg -scf --cleanbuild --skipchecksums` to install the package.

[^2]: don't worry, its very documented. and to clarify the important part: many optimizations displayed in the optimizations section are disabled by default because I know some of you will blindly `makepkg -s` anyway.

That's it, Enjoy the Catgirl Edition of Linux!

