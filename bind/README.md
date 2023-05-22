# BIND9 dockerized service

Here you can find the configuration for my home DNS server.
It serves both as a DNS cache and a LAN name resolver. 

The main purpose of this service is to answer to name queries between hosts running in my LAN. At the time of writing this, all DNS requests from hosts outside my LAN are set to be ignored.

Currently, the `192.168.0.0/16` LAN is configured under the domain `home.`.

Here are some useful tools/links:
 * [latest BIND9 documentation](https://bind9.readthedocs.io/en/latest/chapter1.html)
 * [RNDC documentation](https://manpages.debian.org/bullseye/bind9-utils/rndc.8.en.html): NS control utility

## Running

You can run this service using your preffered `docker-compose` command, but you should probably configure it first.

## Configuration

There should be a stock configuration included with this, with the `.tmp` extension. Rename each file with the extension `.priv`, those will be automatically excluded from version control. You can use them as is, but you should change it to fit your networking needs. 

Changes should be done primarily in the file `zones/db.home.priv` and reflected in the reverse lookup table `zones/db.192.168`.

If you don't understand the syntax used in these files, you should probably brush up in your DNS knowledge :) or consult `Zone files` under the BIND9 documentation.

Besides the default zone (`home.`) configuration, you can also extend other configurations.

### RNDC
This deployment also includes a RNDC server, which might be useful for whatever DNS management purposes you have. By default, the RNDC server is listening in `127.0.0.1` on its default port (`953`) and it's behind a closed container port, so it will be inaccessible outside the container. 

For it to be accessible from outside the container, you would need to open port 953 in the docker container and change the bounded address to something like `0.0.0.0`.
