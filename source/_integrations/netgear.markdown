---
title: NETGEAR
description: Instructions on how to integrate NETGEAR routers into Home Assistant.
ha_category:
  - Presence Detection
  - Update
ha_iot_class: Local Polling
ha_release: pre 0.7
ha_domain: netgear
ha_platforms:
  - button
  - device_tracker
  - sensor
  - switch
  - update
ha_config_flow: true
ha_codeowners:
  - '@hacf-fr'
  - '@Quentame'
  - '@starkillerOG'
ha_ssdp: true
ha_integration_type: integration
---

This platform allows you to detect presence by looking at connected devices to a [NETGEAR](https://www.netgear.com/) device and control the NETGEAR device.
Both routers and access points can be used with this integration. Some access points will not be automatically discovered and need to be set up manually.
Attached devices are only tracked on NETGEAR devices set to the router mode, otherwise, duplicate entities will occur from access points that also report the same devices.

{% include integrations/config_flow.md %}

{% include integrations/option_flow.md %}
{% configuration_basic %}
Consider_home:
  description: "The consider home time is the number of seconds to wait till marking someone as not home after not being seen. This parameter is most useful for households with Apple iOS devices that go into sleep mode while still at home to conserve battery life. iPhones will occasionally drop off the network and then re-appear. This option helps prevent false alarms in presence detection."
{% endconfiguration_basic %}

## Router entities
The NETGEAR router will have the following entities:

### Reboot button

Button entity to restart the router.

### Update entity

Update entity to view current and latest firmware version, and install the latest firmware of the router.

### Traffic meter data

The total and average amount of downloaded/uploaded data through the router can be tracked per day/week/month.
In order for these entities to display the data (instead of 0), the "Traffic Meter" should be enabled in the router settings.
Log into your router > Select **ADVANCED** > **Advanced Setup** > **Traffic Meter** > **Enable Traffic Meter** check box.

### Speed test data

The "Average Ping", "Downlink Bandwidth" and "Uplink Bandwidth" can be tracked by performing a speed test every 30 minutes.
If these sensor entities are enabled they will first show as Unknown since the first speed test does only happen 30 minutes after the integration loads, previous results will be restored on subsequent restarts.
The speed test interval is chosen to be 30 minutes to not put unnecessary load on the network.

### Ethernet link status

The Ethernet link status sensor indicates if the router is currently able to connect to the internet.

### Utilization sensors

CPU and memory utilization sensors in percentage of available resources of the router.

## Connected device entities

For each device connected to the NETGEAR router the following entities will be available:

### Device tracker

Displays if the device is currently connected to the router (Home) or not (Away).

### Allowed on Network

Switch that lets you Allow or Block a device on the Network.
For this entity to actually Block the device, "Access Control" needs to be turned on in the Router settings.
Log into your router > Select **ADVANCED** > **Security** > **Access Control** > **Turn on Access Control** check box.

### Signal strength

Displays the wifi signal strength of the device.

### Link rate

Displays the current link rate of the device indicating the maximum possible data speed with the current connection.

### Link type

Displays the current link type: wired, 2.4GHz or 5GHz.
