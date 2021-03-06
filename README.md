# Zabbix-Templates

Zabbix templates created to monitor some backbone network resources.

## Template Cisco BGP

 - Auto-discovering
 - Supports IPv6 BGP sessions
 - Trigger for 80% prefix limit reached
 - Monitoring of 32-bit ASNs supported
 - Different message/severity based on ASN
 - Trigger disabled when BGP in admin shutdown mode

*This template uses the MIB cbgpPeer2Table, allowing identifying the ASN even when 32-bits. It also allows monitoring IPv6 sessions. The disadvantage of this MIB is that the cbgpPeer2RemoteAddr is an "not-accessible" object, this way, I had to obtain the IP addresses directly from the MIB index structure.*

#### Zabbix Macros:
 - {$BGP_CRITICAL_ASN} - critical ASNs - format ^(00000|11111|22222|33333)$
 - {$SNMP_COMMUNITY} - the router SNMP community

## Template Cisco OSPF

 - Auto-discovering
 - Excludes the loopback interface
 - Monitors the OSPF neighbor status
 - Discovering based on OSPF interfaces

*Monitoring of something that not exists is impossible! That's why is impossible to monitor the OSPF neighbor directly because when the session goes does, the neighbor does not exist anymore, and the Zabbix item gets unsupported. The best way that I found was to monitor the designated router of each OSPF interface. When the OSPF session goes down, the designated router becomes "0.0.0.0" and then I trigger the alert.*

#### Zabbix Macros:
 - {$SNMP_COMMUNITY} - the router SNMP community
