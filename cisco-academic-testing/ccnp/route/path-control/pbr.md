# Policy Based Routing (PBR) :world_map:

* PBR EnableS you to implement policies that selectively cause packets to take different paths:
   +  IP routing is destination-based
   +  PBR overrides destination-based routing

* Applied to incoming or locally generated packets
* Requires a route map to implement the policy :exclamation::
   + Interesting traffic is defined with the match command
   + Destination for interesting traffic is defined with the set command

PBR is used to bypass the routing table. It enables you to configure different routing rules beyond the original IP routing table. One of the ways that it can be used is to route packets that are based on the source IP address instead of the destination IP address. 

PBR is applied to incoming or locally generated packets that are sent by the router itself. PBR is implemented using route maps, for which match commands are used to match the incoming packets, and a subset of the set commands is used to change the default destination-based routing.

* Source-based path selection:
    + Traffic from different users can use different paths for the same destination.
* Load sharing:
    + Forces load sharing without regard to the routing table.

## Use cases

_Source-based transit-provider selection_: ISPs and other organizations use PBR to route traffic that originates from different sets of users through different Internet connections across the policy routers.

_Load sharing_: In addition to the dynamic load-sharing capabilities that are provided by destination-based routing that is supported by Cisco IOS Software, you can implement policies that are based on the traffic characteristics to distribute traffic among multiple paths.

Enable PBR by configuring a route map:
Match traffic using the match command.
Define the action for matched traffic using the set command.

_Apply a route map_:

    To an incoming interface to affect traffic passing through a router.
    To local policy to affect traffic generated by the router.

## Verify the PBR configuration.

You can use requirements from the previous figure to create the implementation plan for PBR configuration. The implementation plan includes the following steps to configure and verify PBR on Cisco route

* Enable PBR by configuring the route map. Match the traffic using the match command with the access list. Then, set the action for manipulating path control using the set command.
* Apply the route map that is created to an incoming interface or to locally generated packets in the router.
* Verify PBR configuration with basic connectivity and path verification commands, and policy routing show commands.


### Example Configuration

#### 1. Create ACL :hammer_and_wrench:

```
BR1# configure terminal
BR1(config)# ip access-list extended PBR-ACL
BR1(config-ext-nacl)# permit ip host 192.168.110.10 any
```

#### 2. Create Route Map :hammer_and_wrench:

```
BR1(config)# route-map PBR-RP
BR1(config-route-map)# match ip address PBR-ACL
```

#### 3. Alter the traffic path :hammer_and_wrench:

Change the next hop with the set ip next-hop route-map subcommand. By setting the next hop to 10.10.10.1, router BR1 will forward all matched traffic over the serial link.

```
BR1(config-route-map)# set ip next-hop 10.10.10.1
```

#### 4. Verify the configured route map :rotating_light:

The route map output states that incoming traffic defined with the access list PBR-ACL is forwarded to 10.10.10.1, which corresponds to the IP address of HQ configured on the serial link.

```
BR1# show route-map
route-map PBR-RP, permit, sequence 10
  Match clauses:
    ip address (access-lists): PBR-ACL
  Set clauses:
    ip next-hop 10.10.10.1
  Policy routing matches: 0 packets, 0 bytes
```

#### 5. Apply the route map to the inbound interface :hammer_and_wrench:

Apply the route map with the ip policy interface-level command. The command should be applied to the inbound interface, that is, to an interface where the traffic is entering the router. If you want to alter the traffic path for locally generated traffic, that is, traffic that is generated by the local router itself, you need to attach the route map with the global configuration mode command ip local policy route-map route-map-name. 

```
BR1(config)# interface ethernet 0/1
BR1(config-if)# ip policy route-map PBR-RP
```

#### 6. Verify the configured policy. :rotating_light:

Use the show ip policy global-level command to verify the configured policies. As you can see from the output, the route map PBR-RP is applied to the Ethernet0/1 interface.

```
BR1# show ip policy
Interface      Route map
Ethernet0/1    PBR-RP
```

#### 7. Enable PBR Debugging :rotating_light:

Enable PBR debugging on BR1 to analyze the detailed policy-based routing operation. Initiate traffic from the Notebook and the PC to the HQ router using ICMP. To verify the actual traffic path in the lab environment, you can use the debug ip policy command. For the command to display the output, traffic must be present on the network. If that is not the case, you must generate traffic, with the ping command, for example.

```
BR1# debug ip policy
Policy routing debugging is on
```