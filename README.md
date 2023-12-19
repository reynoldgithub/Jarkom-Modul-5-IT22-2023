# Jarkom-Modul-5-IT22-2023

# First Configuration
## Subnetting and Routing
![image](https://github.com/reynoldgithub/Jarkom-Modul-5-IT22-2023/assets/87769109/1c69ce9e-744b-4bcd-b150-ebb576af8eb4)
Berikut network configuration untuk setiap node
- Revolter
```
auto eth0
iface eth0 inet static
	address 192.244.14.130
	netmask 255.255.255.252
	gateway 192.244.14.129
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
- Fern
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.244.14.2
	netmask 255.255.255.128
	up echo nameserver 192.168.122.1 > /etc/resolv.conf


# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.244.14.129
	netmask 255.255.255.252
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.244.14.133
	netmask 255.255.255.252
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

```
- Richter
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.244.14.134
	netmask 255.255.255.252
	gateway 192.244.14.133
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

```
- SchwerMountain
```
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
          hostname schwermountain
```
- Himmel
```

# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.244.12.137
	netmask 255.255.255.252
	up echo nameserver 192.168.122.1 > /etc/resolv.conf


# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.244.14.1
	netmask 255.255.255.128
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.244.12.1
	netmask 255.255.254.0
	gateway 192.168.2.1
	up echo nameserver 192.168.2.1 > /etc/resolv.conf

```
- LaubHills
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.244.12.2
	netmask 255.255.254.0
	gateway 192.244.12.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

```
- Frienren
```


# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.244.14.145
	netmask 255.255.255.252
	up echo nameserver 192.168.122.1 > /etc/resolv.conf


# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.244.12.138
	netmask 255.255.255.252
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.244.14.141
	netmask 255.255.255.252
        gateway 192.244.14.142
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

```
- Stark
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.244.14.146
	netmask 255.255.255.252
	gateway 192.244.14.145
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

```
- Aura
```
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
	hostname Aura

# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.244.14.142
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.244.14.149
	netmask 255.255.255.252
```
- Heiter
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.244.14.150
	netmask 255.255.255.252
	gateway 192.244.14.149
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.244.8.1
	netmask 255.255.252.0
	up echo nameserver 192.168.122.1 > /etc/resolv.conf


# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.244.0.1
	netmask 255.255.248.0
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

# Static config for eth3
#auto eth3
#iface eth3 inet static
#	address 192.168.3.2
#	netmask 255.255.255.0
#	gateway 192.168.3.1
#	up echo nameserver 192.168.3.1 > /etc/resolv.conf

# DHCP config for eth3
#auto eth3
#iface eth3 inet dhcp
#	hostname ubuntu-1-11

```
- Turk Region
```
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
	hostname turkregion
```
## DHCP Server
Tambahkan interface yang digunakan untuk menerima request client DHCP
```
# /etc/default/isc-dhcp-server
.
.
INTERFACESv4="eth0"
.
.
```
Buat dhcp rule config sesuai dengan subnet dan routing
```
# /etc/dhcp/dhcpd.conf
ddns-update-style none;

option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

log-facility local7;


#A1
subnet 192.244.14.128 netmask 255.255.255.252 {
}

#A2
subnet 192.244.14.132 netmask 255.255.255.252 {
}

#A7
subnet 192.244.14.144 netmask 255.255.255.252 {
}

#A5
subnet 192.244.12.136 netmask 255.255.255.252 {
}

#A6
subnet 192.244.14.140 netmask 255.255.255.252 {
}

#A8
subnet 192.244.14.148 netmask 255.255.255.252 {
}

#A3
subnet 192.244.14.0 netmask 255.255.255.128 {
  range 192.244.14.3 192.244.14.126;
  option routers 192.244.14.1;
  option routers 192.244.14.2;
  option broadcast-address 192.244.14.127;
  option domain-name-servers 192.244.14.134;
  default-lease-time 720;
  max-lease-time 7200;
}

#A4
subnet 192.244.12.0 netmask 255.255.254.0 {
  range 192.244.12.2 192.244.13.254;
  option routers 192.244.12.1;
  option broadcast-address 192.244.13.255;
  option domain-name-servers 192.244.14.134;
  default-lease-time 720;
  max-lease-time 7200;
}

#A9
subnet 192.244.0.0 netmask 255.255.248.0 {
  range 192.244.0.2 192.244.7.254;
  option routers 192.244.0.1;
  option broadcast-address 192.244.7.255;
  option domain-name-servers 192.244.14.134;
  default-lease-time 720;
  max-lease-time 7200;
}

#A10
subnet 192.244.8.0 netmask 255.255.252.0 {
  range 192.244.8.3 192.244.11.254;
  option routers 192.244.8.1;
  option broadcast-address 192.244.11.255;
  option domain-name-servers 192.244.14.134;
  default-lease-time 720;
  max-lease-time 7200;
}

```
## DHCP Relay
Aktifkan ip forwarding pada /etc/systctl.conf
```
.
.
net.ipv4.ip_forward=1
.
.
```
Buat config dhcp relay
```
# /etc/default/isc-dhcp-relay
SERVERS="192.244.14.130"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""

```
## DNS Server
Buat DNS forward server
```
# /etc/bind/named.conf.options
options {
  directory "/var/cache/bind";
  forwarders {
    192.168.122.1;
  };
  allow-query {any;};
  auth-nxdomain no;
  listen-on-v6 {any;};
};
```

