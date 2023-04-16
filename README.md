# victron-home-assistant-mqtt
Home Assistant Integration for Victron GX devices using MQTT bridging

# Setup / Installation

## Mosquitto

You will need to run a mosquitto broker. To integrate it with Victron MQTT,
enable MQTT on your Victron device under

 - Settings
   - Services
     - MQTT on LAN (Plaintext)

Then, configure your Moquitto server to connect to it. The easiest way is
to copy the file `mosquitto/conf.d/victron.conf` to `/etc/mosquitto/conf.d`
and change the line
```
address victron-ip-address
```
to have the IP address or hostname of your Victron system instead of
`victron-ip-address`. Then, restart moquitto.

## Home Assistant
Make sure you have configured Home Assistant to use packages by including
this snippet in your `configuration.yaml` file:
```
homeassistant:
  packages: !include_dir_named packages
```

Then, copy everything from the `ha` directory into your Home Assistant
configuration directory.

Finally, you will need to adjust the file `victron_mqtt/automation/keepalive.yaml`
and change the line
```
      topic: victron/R/vrm-portal-id/keepalive
```
to have your actual VRM portal ID instead of `vrm-portal-id`. You can find this
in your Victron device at

 - Settings
   - VRM online portal
     - VRM Portal ID

# Limitations
Currently, this supports only one item of each kind (one inverter, one
solar charger, one battery etc.)

Eventually I'd like to make this a proper extension, PRs are welcome to
either extend the functionality of this approach or make it a real
extension that could be deployed via HACS.
