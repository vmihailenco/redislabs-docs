---
title: Get started with Redis Enterprise Software
linkTitle: Get started
description:
weight: 1
alwaysopen: false
categories: ["RS"]
aliases: [
    /rs/getting-started/quick-setup/,
    /rs/getting-started/,
    /rs/getting-started.md,
    /rs/installing-upgrading/get-started-redis-enterprise-software.md,
    /rs/installing-upgrading/get-started-redis-enterprise-software/,
    ]
---
This guide helps you install Redis Enterprise Software on a Linux host to test its capabilities.

When finished, you'll have a simple cluster with a single node:

- Step 1: Install Redis Enterprise Software
- Step 2: Set up a Redis Enterprise Software cluster
- Step 3: Create a new Redis database
- Step 4: Connect to your Redis database

{{< note >}}
**This quick start is designed for local testing only.**
For production environments, the [install and setup]({{< relref "/rs/installing-upgrading/_index.md" >}}) guide  walks through deployment options appropriate for a production environment.
{{< /note >}}

Quick start guides are also available to help you:

- Run Redis Software using a [Docker container]({{< relref "/rs/installing-upgrading/get-started-docker.md" >}}), which lets you skip the installation process
- Set up a [Redis on Flash cluster]({{< relref "/rs/databases/redis-on-flash/getting-started-redis-flash.md" >}}) to optimize  memory resources
- Set up an [Active-Active cluster]({{< relref "/rs/databases/active-active/get-started.md" >}}) to enable high availability
- [Benchmark]({{< relref "/rs/clusters/optimize/memtier-benchmark.md" >}}) Redis Enterprise Software performance.

## Step 1: Install Redis Enterprise Software

To install Redis Enterprise Software:

1. Download the installation files from the [Redis Enterprise Download Center](https://www.redislabs.com/download-center/)
and copy the download package to machine with a Linux-based OS. To untar the image:

    ```sh
    tar vxf <downloaded tar file name>
    ```

    {{< note >}}
You are required to create a free login to access the download center.
    {{< /note >}}

1. Once the tar command completes, run the `install.sh` script in the current directory.

    ```sh
    sudo ./install.sh -y
    ```

### Port availability

If port 53 is in use, the installation fails. This is known to happen in
default Ubuntu 18.04 installations where `systemd-resolved` (DNS server) is running.
To workaround this issue, change the system configuration to make this port available
before installing Redis Enterprise Software.

Here's one way to do so:

1. Run: `sudo vi /etc/systemd/resolved.conf`
1. Add `DNSStubListener=no` as the last line in the file and save the file.
1. Run: `sudo mv /etc/resolv.conf /etc/resolv.conf.orig`
1. Run: `sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf`
1. Run: `sudo service systemd-resolved restart`


## Step 2: Set up a cluster

To set up your machine as a Redis Enterprise software cluster:

{{< embed-md "cluster-setup.md" >}}

## Step 3: Create a database

1. Select "redis database" and the "single region" deployment, and click Next.

    ![Redis Enterprise Software create database](/images/rs/getstarted-newdatabase.png)

1. Enter a database name such as `database1` and then select **Show Advanced Options**.

    ![Redis Enterprise Software configure new database screen](/images/rs/getstarted-createdatabase.png)

1. In **Endpoint port number**, enter `12000`.

1. Select the **Activate** button to create your database.

You now have a Redis database!

## Step 4: Connect to your database

After you create the Redis database, you are ready to store data in your database.
See [test connectivity]({{<relref "/rs/databases/connect/test-client-connectivity.md">}}) page for a tutorial on connecting to your database.

## Supported web browsers

To use the Redis Software admin console, you need a modern browser with JavaScript enabled.

The following browsers have been tested with the current version of the admin console:

- Microsoft Windows, version 10 or later.
    - [Google Chrome](https://www.google.com/chrome/), version 48 and later
    - [Microsoft Edge](https://www.microsoft.com/edge), version 20 and later
    - [Mozilla Firefox](https://www.mozilla.org/firefox/), version 44 and and later
    - [Opera](https://www.opera.com/), version 35 and later.

- Apple macOS:
    - [Google Chrome](https://www.google.com/chrome/), version 48 and later
    - [Mozilla Firefox](https://www.mozilla.org/firefox/), version 44 and and later
    - [Opera](https://www.opera.com/), version 35 and later.

- Linux:
    - [Google Chrome](https://www.google.com/chrome/), version 49 and later
    - [Mozilla Firefox](https://www.mozilla.org/firefox/), version 44 and and later
    - [Opera](https://www.opera.com/), version 35 and later.


## Next steps

Now you have a Redis Enterprise cluster ready to go. You can connect to it with
a [redis client](https://redis.io/clients) to start loading it with data or
you can use the [memtier_benchmark Quick Start]({{< relref "/rs/clusters/optimize/memtier-benchmark.md" >}})
to check the cluster performance.
