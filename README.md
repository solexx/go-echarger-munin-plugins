### Background

These are [Munin](http://munin-monitoring.org/) plugins for monitoring
[go-eChargers](https://go-e.co/) for electric vehicles. They are using
the device's local API. That means the device needs to be accessible
from the LAN.  Authentication against go-e's cloud service is not
supported.

The plugins make a lot of requests to the device, but I haven't noticed
any problems with that yet.

### Plugins

- **go_echarger_charging** Displays state of current charge and a
  possibly configured limit.
- **go_echarger_current** Displays currents (in Ampere) of all three
  lines, the current supported by an attached cable, the configured
  limit (may be changed by pressing the button on the device)  as well
  as the absolute maximum current supported by the charger.
- **go_echarger_efficiency** Display efficiency factor per line.
- **go_echarger_energy** Displays the total energy output (in kWh) by
  the device as well as per individual RFID token slot.
- **go_echarger_power** Displays the current power output (in kW) per
  line and in total.

### Setup

Just drop the plugins into `/etc/munin/plugins` and restart `munin-node`. 

Unless your go-eCharger can be reached with the hostname
`go-echarger` you need to add this somewhere in
`/etc/munin/plugin-conf.d/` with the proper hostname or IP address:

```
[go-echarger-*]
env.host go-echarger.home.well-adjusted.de
```

None of the plugins need any special privileges. There is no need to run
them as root.

You need to have `jq` installed as this tool is used for parsing the
JSON returned by the charger's API.

### Examples

Here's my setup with all default graphs:
https://jigsaw.home.well-adjusted.de/munin/go_echarger-week.html

### TODO

- [ ] Add TODOs ;-)

### Contact

For questions and support, feel free to use the Issue Tracker or drop me an
e-mail at js+github at wim.re.
