# vagrant-sad

Vagrant Search and Destroy, AKA "I'm v sad that Vagrant ate my box".

Using Vagrant for CI risks leaving a lot of stuff behind (both as running VMs and data on disk), this repo contains some solutions to making that more manageable.

It's intended mainly as a glue layer between Gitlab-CI and Vagrant when VirtualBox VMs are in use.

# Dependencies

 * Vagrant
 * VirtualBox
 * [bash](https://www.gnu.org/software/bash/) (not posix shell, I actually mean bash)

# Scripts

## clean-up-vbox-vms

This is a safety net, it's assumed that you're setting up your CI jobs to at least *try* to clean up after themselves, but if they don't you can execute this from cron intermittently to catch failed clean ups.

Cleans up old Virtual Box VMs.

Usage:

```
$ max_run_age=N max_off_age=N ./clean-up-vbox-vms
```

e.g to power off VMs that have been running more than 1 hour:

```
$ max_run_age=3600 ./clean-up-vbox-vms
```

to remove VMs that have been hanging around on disk (not running) for more than 1 day:

```
$ max_off_age=86400 ./clean-up-vbox-vms
```

Note: it's assumed that `max_off_age` will only be used when a smaller `max_run_age` is supplied.