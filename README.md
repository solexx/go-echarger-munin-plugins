### Background

These are [Munin](http://munin-monitoring.org/) plugins for monitoring
[go-eChargers](https://go-e.co/) for electric vehicles. They are using the
device's local [API](https://github.com/goecharger/go-eCharger-API-v1). That
means the device needs to be accessible from the LAN.  Authentication against
go-e's cloud service is not supported.

The plugins make a lot of requests to the device, but I haven't noticed
any problems with that yet.

### Plugins

- **go_echarger_charging** Displays state of current charge, a possibly
  configured limit and optionally your battery's capacity (see the Setup
  section below).
- **go_echarger_current** Displays currents (in Ampere) of all three lines, the
  current supported by an attached cable, the configured limit (may be changed
  by pressing the button on the device)  as well as the absolute maximum
  current supported by the charger.
- **go_echarger_efficiency** Display efficiency factor per line.
- **go_echarger_energy** Displays the total energy output (in kWh) by the
  device as well as per individual RFID token slot.
- **go_echarger_power** Displays the current power output (in kW) per line and
  in total.
- **go_echarger_state** Displays various status fields that the device reports.
- **go_echarger_temp** Displays all temperatures that the (current/new gen)
  device reports.

### Setup

Just drop the plugins into `/etc/munin/plugins` and restart `munin-node`. 

Unless your go-eCharger can be reached with the hostname
`go-echarger` you need to add this somewhere in
`/etc/munin/plugin-conf.d/` with the proper hostname or IP address:

```
[go_echarger_*]
env.host go-echarger.home.well-adjusted.de
```

You can also optionally set your EV's battery capacity in kWh to have it
displayed as a constant in the charging graph:

```
[go_echarger_*]
env.capacity 28
```


None of the plugins need any special privileges. There is no need to run
them as root.

You need to have `jq` installed as this tool is used for parsing the
JSON returned by the charger's API.

### Examples

Here's my setup with all default graphs:
https://jigsaw.home.well-adjusted.de/munin/go_echarger-week.html

### TODO

- [X] Make only one API request per plugin execution
- [X] Add configuration for battery capacity to display in the charging
  plugin

### Contact

For questions and support, feel free to use the Issue Tracker or drop me an
e-mail at js+github at wim.re.
