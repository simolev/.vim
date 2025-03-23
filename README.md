# Network issue summary

Hi Content Team, here's an outline of the issues and how we tackled them.

#|affected machine | area | description | resolution
-|-|-|-|-
1|client & server | wireguard config | <ul><li>wrong subnet defined on the client</li><li>missing `6pn` peer addresses</li><li>mismatched MTUs</li></ul> | corrected the configs (subnet `192.168.0.0`, default MTU) and reset the Wireguard link
2|client & server | firewall | `ipv6` rule blocking the Wireguard port `51820` |deleted the rule
3|client | routes | route for the Wireguard subnet on the wrong interface `192.168.0.0/24 via 172.19.5.10 dev eth0`| deleted the route
4|server | system setting | ignore ping requests | set `net.ipv4.icmp_echo_ignore_all=0`
5|server| firewall |  rule blocking incoming `ipv4` on port `8080` on the Wireguard interface | deleted the rule
6|server| firewall | reachable over the plain old `6pn` network | added a firewall rule to block incoming `ipv6` on the app port `8080`

Additionally, we realized there was an issue in one of our troubleshooting scripts. We quickly fixed the tool as soon as we realized it was giving wrong results, but this certainly contributed to slowing us down a tiny bit during the early phases of our investigation. Please consider whether to include this information.
