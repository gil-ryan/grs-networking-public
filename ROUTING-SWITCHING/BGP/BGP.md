# BGP - Border Gateway Protocol

## External Neighbors

### Prequisites

* BGP ASN
* Router configuration mode

<pre>
neighbor _ip-address_ remote-as _autonomous-system-number_
neighbor _ip-address_ description _EXTERNAL NEIGHBOR [IP] - [ASN NAME] - [ASN #]_
</pre>

Example:

```
configure terminal
router bgp 64512
neighbor 1.1.2.2 remote-as 64513
neighbor 1.1.2.2 description EXTERNAL NEIGHBOR 1.1.2.2 - verizon datacenter - AS64513
```

### Shutdown External Neighbor

```
neighbor ip-address shutdown
```

Example:

```
neighbor 1.1.2.2 shutdown
```