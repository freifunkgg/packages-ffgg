# cleanup-gluon-config

Mit diesem Package werden auf einem Freifunkknoten alte und überflüssige Konfigurations-Artefakte entfernt. 

Hierdurch ist es bei Bestandsknoten sehr einfach möglich, dass ohne frisches Aufsetzen der Knoten z.B. innerhalb einer Community ein Technologie-Wechsel ( z.B. VPN-Protokolls oder Mesh-Protokoll) oder ein Knotenumzug von einer Community zu einer anderen Community durchgeführt werden kann.

Ein `'sysupgrade -n'` mit einer gefolgten Neukonfiguration im Konfigmodus ist nicht notwendig. 

Prinzipiel sichert das Package die wichtigsten vom User veränderten/angepassten UCI-Parameter, löscht dann das OverlayFS und schreibt die User UCI-Parameter wieder zurück. Nach dieser Prozedur verhält sich der Knoten wie ein frisch konfigurierter Knoten.

Die Prozedur ist mehrphasig. Der Router startet nach einem normalem '`sysupgrade`' bzw. '`autoupgrade`' in Summe 4 mal neu durch (Anmerkung: 5 mal nach einem 'firstboot').  

Die Prozedur dauert je nach Hardware ca. 5 Minuten (+/-).

Der generelle und dauerhafte Einsatz dieses Package in einer Community-Firmware ist nicht angedacht. Eine Firmware mit diesem Packages sollte nur als zeitlich beschränkter Übergang zu einer neuen Firmware-Version dienen. Die Verbreitung einer Factory-Firmware mit diesem Packages ist nicht zu empfehlen. 

---

### Falls vorhanden, so werden folgende vorherige Konfigurationen übernommen:
  
  - Die Datei `/etc/rc.local`
  - Die Dropbear-Dateien `authorized_keys` und `dropbear_rsa_host_key`
  - Hostname
    - system.@system[0].hostname
    - system.@system[0].pretty_hostname
  - Nodeinfo
    - gluon-node-info.@owner[0].contact
    - gluon-node-info.@location[0].share_location
    - gluon-node-info.@location[0].latitude
    - gluon-node-info.@location[0].longitude
    - gluon-node-info.@location[0].altitude
  - Static IPv4 & DHCP
    - network.wan.proto
    - network.wan.ipaddr
    - network.wan.netmask
    - network.wan.gateway
  - static DNS
    - gluon-wan-dnsmasq.@static[0].server
  - VPN bandwidth limitation
    - gluon.mesh_vpn.limit_egress
    - gluon.mesh_vpn.limit_ingress
    - gluon.mesh_vpn.limit_enabled
  - VPN
    - fastd.mesh_vpn.enabledd
  - MoL / MoW
    - network.mesh_wan.disabled
    - network.mesh_lan.disabled
  - PoE
    - system.gpio_switch_poe_passthrough.value
  - Wifi
    - gluon.wireless.outdoor
    - gluon-core.@wireless[0].preserve_channels
    - wireless.radio0.channel
    - wireless.radio1.channel
    - wireless.radio0.disabled
    - wireless.radio1.disabled
    - wireless.client_radio0.disabled
    - wireless.client_radio1.disabled
    - wireless.mesh_radio0.disabled
    - wireless.mesh_radio1.disabled

---

## Einbindung in Gluon
Wird das Package in der Firmware eingebunden, dann muss dafür gesorgt werden, dass der Konfigmodus übersprungen wird. Das Aufspielen einer Factory-Firmware auf einen neuen Router wird daher zu einem mit Default-Werten konfigurierten Router führen. 

Wird dieses Package in der `site.mk` eingebunden, dann muss folgender Eintrag in der `site.conf` vorhanden sein

```
...
  setup_mode = {
    skip = true,
    },
...
```

---

## ToDo
Die Vorgaben der zu sichernden Parameter in die `site.conf` verlagern.
