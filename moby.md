# Moby (aka Docker aka Docker Engine aka Engine+CLI)

- CLI back under github.com/docker/docker
	- the split causes development headaches (have to coordinate repo changes)
	- the CLI is *literally* the ops "API" to the Engine - it's kind of insane to maintain it separately

- moar OCI layouts support (if you squint, they're "just" an on-disk registry)
	- `docker pull` from and `docker push` to an OCI layout on-disk directly
	- `docker pull` from an OCI layout in a tar file on disk
	- `docker run` an OCI layout directly (either directory or tarball)

- direct rootfs support
	- `docker run` a rootfs directly ("super `chroot`") - I currently use `systemd-nspawn` for this, but it has a *lot* of very rough/sharp edges

- split TTY handling (`--tty` is all-or-nothing, and I'd like to say "tty for stdin+stderr only" for example)
	- some CLIs are like `sudo` and to use them requires sending output to stdout, but still using stderr + stdin's TTY to prompt for a password
	- think `value="$(sudo ...)"` except it's `value="$(docker run --tty=stdin ...)"`

- `--rm` should be enabled-by-default unless `--detach` is specified

- `--interactive` should just be straight up enabled-by-default
	- related, it's got some poor Ctrl-C vs signal handling behavior that could use some work/attention (because Ctrl-C is a TTY thing)

- explicit support for X11 and creating a secure proxy for it (maybe Wayland is better at/for this?)

- better/simpler Network Plugins so that something like Tailscale can be integrated cleanly/easily without weird sidecar containers

- simpler "easy mode" Mount/Volume Plugins
	- for many cases, it would be "enough" to have a way to say "run X command inside a container of Y image and pass it Z data and it will run/provide a mounted volume"
	- for example, `sshfs` or NFS (or any FUSE filesystem) would be trivial this way, assuming we can get `--device /dev/fuse` too

- destroy the "managed plugin containers" concept - even the containers above should just be normal containers, even if they're hidden from `docker ps` by default

- container startup ordering (especially for plugins implemented by containers)

- overlay networks without Swarm
	- overlay networks using WireGuard (see also "network plugins" note above)
