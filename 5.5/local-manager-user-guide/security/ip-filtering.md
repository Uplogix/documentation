<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager summary page > Network > Protocols</div>

By default, the Local Manager allows access from any IP address; however, access can be restricted to certain IP addresses or networks by using the **config system protocols filter** command. This command opens an editor that allows you to explicitly permit and deny access to source IP addresses and networks.

For example, specify your management subnet or your own computer and then use the **deny all** subcommand to block any IP address not explicitly allowed. This blocks all new communication with the Local Manager that is not sourced from the permitted IP address or network.

The filter automatically adds defined services such as the Control Center, TACACS, RADIUS, and NTP servers, as well as each deviceâ€™s specified management or dedicated IP address to the list of allowed IP addresses.

Filters are applied during both in-band and out-of-band communications.

Use the **allow** and **deny** subcommands to specify networks. Use the no modifier to remove previously configured behavior.

```
[admin@UplogixLM]# config system protocols filter
[config system protocols filter]# deny 192.0.2.1
[config system protocols filter]# deny 198.51.100.0/24
[config system protocols filter]# deny 203.2.0.0/16
[config system protocols filter]# deny 203.0.0.0/8
[config system protocols filter]# allow 198.51.100.254
[config system protocols filter]# no allow 198.51.100.254
```

Filtering subtracts the sum of the deny statements from the sum of allow statements.

Filtering only applies to new connections. If you deny an IP address while a user at that address has a CLI session open, the connection will not be affected. However, the user will not be able to open a new session.

Filters are applied after you exit the editor.