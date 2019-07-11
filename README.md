#### xip-pdns

This is the source of the [PowerDNS](http://powerdns.com/) pipe backend adapter powering [xip.io](http://xip.io/).

Install this on your system, adjust [etc/xip-pdns.conf](etc/xip-pdns.conf.example) to your liking, and configure PowerDNS as follows:

    launch=pipe
    pipe-command=/path/to/xip-pdns/bin/xip-pdns /path/to/xip-pdns/etc/xip-pdns.conf


#### Nuvyyo Setup

1. Set up an AWS EC2 server with a static (Elastic) IP address.
2. Update, upgrade, and install `pdns-server pdns-backend-pipe`.
3. Clone this repository into `/etc/xip-pdns`.
4. Provide a configuration, eg. by modifying `xip-pdns.conf.example` and
   pointing to the file from the PowerDNS configuration (see above section).
5. On Ubuntu, run `systemctl disable systemd-resolved` as it runs on port `53`
   by default, which is needed by PowerDNS.
6. Remove the now-empty `/etc/resolv.conf` symlink, and create a new file
   containing a valid name server (eg. `nameserver 8.8.8.8`).
7. Restart the server, everything should now be working. Testing can be done
   via `dig` or `nslookup`. For example (with a server IP of 10.1.2.3):

   `dig +short iphone.234-42-52-12.dns-resolve.tablotv.com @10.1.2.3`

   `nslookup dns-resolve.tablotv.com 10.1.2.3`
