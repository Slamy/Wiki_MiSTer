MiSTer board can be access through on-board Ethernet port. System has **FTP**, **SSH**, **SFTP** services running.

User name: **root**  Password: **1**

When using FTP, make sure your file transfers are in Binary not ASCII. ASCII-type transfers will result in corruption of that data. A good FTP client for Windows that defaults to Binary and supports FTP as well as SFTP and SCP (ssh copy) is [WinSCP](https://winscp.net/eng/download.php).

By default, DHCP is used to acquire an IP address for the board.
You can find it from your router (easier way), or from console connected to the board using the command **ifconfig**

The default MAC address for the on-board Ethernet port is `02:03:04:05:06:07`. Please consider this when connecting more than one MiSTer board via the on-board Ethernet port to your network.

> TODO: How to setup a custom MAC address.

## Setting up a static IP address

`dhcpcd` is currently the easiest way to set up static IPs. You can add a new static address profile by editing the `/etc/dhcpcd.conf` file and adding a new block defining the static IP. For example adding:

    interface wlan0
    static ip_address=192.168.0.64/24
    static routers=192.168.0.1
    static domain_name_servers=8.8.8.8 1.1.1.1

to the bottom of `/etc/dhcpcd.conf` defines a new static IP for the `wlan0` (wi-fi) interface. It has the static IP `192.168.0.64` and points to the router/gateway at `192.168.0.1` with DNS coming from `8.8.8.8` and `1.1.1.1` as a secondary option. 

After a quick restart of the MiSTer you should be able to verify these new static IPs by running the command `ip address`:

    /root# ip address
    [...]
    3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
        link/ether 28:87:ba:39:aa:9d brd ff:ff:ff:ff:ff:ff
        inet 192.168.0.6/24 brd 192.168.0.255 scope global wlan0
           valid_lft forever preferred_lft forever
        inet 192.168.0.64/24 brd 192.168.0.255 scope global secondary noprefixroute wlan0
           valid_lft forever preferred_lft forever

As seen here, the `192.168.0.64` address is now assigned to this interface. Above that is IP assigned dynamically (`192.168.0.6`).

> You can also setup your on-board network connection by editing `/etc/network/interfaces`. This is currently not advised. Because if you have a DHCP server in your network, the network stack will still contact the DHCP server and assign the returned IP address regardless, leading to usually unwanted behavior.

## Other

**mc** (midnight commander) file manager is available for easier folder navigation.

The root of SD card: **/media/fat**

Related: [Serial Console Access](Console-connection)
