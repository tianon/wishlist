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
