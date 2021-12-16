## ubuntu 14.04

```
interfaces gre

auto test1
iface test1 inet tunnel
        address 172.18.1.2
        netmask 255.255.255.252
        mode gre
        endpoint 1.1.1.1
        dstaddr 172.18.1.1
        local 192.168.104.80
        ttl 255
      
```

​	

## ubuntu 20.04

gre

```
/etc/systemd/network/gretest.network:

[Match]
Name=gretest
[Network]
Tunnel=gretest
```

```
/etc/systemd/network/gretest.netdev:

[Match]                                         
[NetDev]                                                  
Name=gretest
Kind=gre

[Tunnel]
Independent=true                                            
Local=192.168.1.106 
Remote=184.105.250.46
TTL=255
```

```


/etc/netplan/gretest.yaml :

network:
  version: 2
  renderer: networkd
  ethernets:
      gretest:
          dhcp4: no
          dhcp6: no
          addresses: 
               - 172.22.1.1/24
```
