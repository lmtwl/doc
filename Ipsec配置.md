## IPsec 配置

### tunnel

##### ipsec.conf

```
conn netbar-m
        authby=secret
        left=180.163.61.114
        leftsubnet=172.22.3.254/32
        right=%any
        rightsubnet=172.22.1.254/32
        ike=aes256-sha2_256-modp1024!
        esp=aes256-sha2_256!
        keyingtries=0
        ikelifetime=1h
        lifetime=24h
        dpddelay=30
        dpdtimeout=120
        dpdaction=restart
        auto=start
conn netbar-s
        authby=secret
        left=180.163.61.114
        leftsubnet=172.22.3.254/32
        right=%any
        rightsubnet=172.22.10.254/32
        ike=aes256-sha2_256-modp1024!
        esp=aes256-sha2_256!
        keyingtries=0
        ikelifetime=1h
        lifetime=24h
        dpddelay=30
        dpdtimeout=120
        dpdaction=restart
        auto=start
```



```
config setup

conn ShangHai-txy
        authby=secret
        left=%defaultroute
        leftid=%any
        leftsubnet=192.168.1.106/32
        #right=121.4.141.48
        #rightsubnet=192.168.62.87/32
        ike=aes256-sha2_256-modp1024!
        esp=aes256-sha2_256!
        keyingtries=0
        ikelifetime=1h
        lifetime=8h
        dpddelay=30
        dpdtimeout=120
        dpdaction=restart
        auto=start
conn M
        also=ShangHai-txy
        right=121.4.141.47
        rightsubnet=192.168.62.87/32
conn S
        also=ShangHai-txy
        right=121.4.141.49
        rightsubnet=192.168.62.88/32
```

##### ipsec.secrets

```
# This file holds shared secrets or RSA private keys for authentication.

# RSA private key for this host, authenticating it to any other host
# which knows the public part.
#221.237.152.64 106.15.201.93 : PSK "123" 
# ipsec.secrets - strongSwan IPsec secrets file
: RSA server.pem
: PSK "redhat@234"
: XAUTH "redhat@234"
#Public %any : EAP "password"
##%any %any : PSK "123"
%any %any : PSK "redhat@234"
Public: XAUTH "password"
```



### Transport

##### ipsec.conf

```
# ipsec.conf - strongSwan IPsec configuration file

# basic configuration

config setup
        # strictcrlpolicy=yes
         charonstart = yes
         plutostart = yes
         nat_traversal = yes
         uniqueids = yes
conn ios
        keyexchange=ikev1
        authby=xauthpsk
        xauth=server
        left=%defaltroute
        leftsubnet=0.0.0.0/0
        leftfirewall=yes
        right=%any
        rightsubnet=172.18.1.0/24
        rightsourceip=172.18.1.0/24
        pfs=no
        auto=add
conn L2TP-PSK-NAT
    rightsubnet=vhost:%priv
    also=L2TP-PSK-noNAT

conn L2TP-PSK-noNAT
    authby=secret
    pfs=no
    auto=add
    keyingtries=3
    #rekey=no
    ikelifetime=8h
    keylife=1h
    type=transport
    left=192.168.102.177
    leftprotoport=17/1701
    right=%any
    rightprotoport=17/%any
conn win
    keyexchange=ikev2
    ike=aes256-sha1-modp1024!
#   esp=aes256-sha1!
    dpdaction=clear
    dpddelay=300s
    rekey=no
    left=%defaultroute
    leftsubnet=0.0.0.0/0
    leftauth=pubkey
    leftcert=server.cert.pem
#   leftid="C=CH, O=strongSwan,192.168.1.110" 
    right=%any
    rightsourceip=172.16.112.0/22
#   rightauth=eap-mschapv2
    rightauth=eap-radius
    rightsendcert=never
    eap_identity=%any
    auto=add
conn mac
     keyexchange=ikev1
     authby=xauthpsk
     xauth=server
#    rightauth=eap-radius
#    left=%defaltroute
     leftsubnet=0.0.0.0/0
     leftfirewall=yes
     right=%any
     rightdns=8.8.8.8
     rightsubnet=172.16.128.0/22
     rightsourceip=172.16.128.0/22
     pfs=no
     eap_identity=%any
     auto=add
```

##### ipsec.secrets

```
:   PSK "redhat@234"
#;43.230.88.2  %any:   PSK "redhat@234"
#SERVER-IP %any:   PSK "redhat@234"
Public %any : EAP "password
```

