# Puppet LXC container management class

## Abstract

This class provides LXC container management functionality for Puppet. Features

* Creating and destroying containers on LVM volumes
* Starting and stopping containers
* Configuring container autostart

*Warning!* This has only been tested on Ubuntu 12.04. Use at your own risk!

## Usage

Ensuring a container is created with a given template:

    lxc::container {
        test01:
            ensure     => running,
            template   => "ubuntu",
            vgname     => "lxc",
            host       => "host01",
            autostart  => true,
            lvsize     => 5,
            filesystem => "ext4";
    }

Ensuring a container does not exist on the given host:

    lxc::container {
        test01:
            ensure     => absent,
            host       => "host01";
    }

Ensuring a container does not exist on any host:

    lxc::container {
        test01:
            ensure     => absent;
    }

### Parameters:

* *ensure:* can be 'absent', 'stopped' or 'running'. Defaults to 'running'.
* *template:* the name of your template name.
* *vgname:* the volume group to create your container in.
* *host:* the host to create/destroy your container on. Migration is not (yet?) supported. Defaults to all hosts.
* *autostart:* Automatically start container at boot time. Defaults to true.
* *lvsize:* The logical volume size in GB. Resizing is not supported (yet?). Defaults to 5.
* *filesystem:* The filesystem to use for the container. Defaults to 'ext4'

## Copyright and License

Copyright (C) 2012 Janos Pasztor <business@janoszen.com>

You are free to use this module under the terms of the BSD license.
