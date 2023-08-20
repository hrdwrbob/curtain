# Plumb Jammer

## What is it.

Plumb Jammer is a Library that sits over the top of pipewire and wire plumber that simplifies and abstracts away all the ports and focuses on virtual devices (Plumbs) that can be plugged (jammed) into each other. Filters are able to be defined for any Plumb, as in or out (which applies to all connections), and for pairs of Plumbs. Plumbs are persistant (even if their backing object isn't present), so any application that is used can now be configured and routed even if it's not running.

### Curtain 
Plumb Jammer is a relatively simple library with no front end, because it's intended to be used with  Curtain and Wizard. Wizard provides a dyanmic rule based management system, and runs locally on all curtain clients. 

For full functionality, [Curtain Manager](curtain.md) and [Surface Presser](surfacepresser.md)) are recommended. This provides the advanced ruleset management, as well as a nice user interface to both configure and jam plumbs. 



## Raison d'etre

Problems Plumb Jammer aims to solve:
* pipewire and wireplumber configuration is extremely laborious, and difficult to interface with.
* current effects libraries work really well for the simple/normal case (eg: easyeffects), and are extremely complex for anything else.
* in many audio systems (like pipewire and windows) the config may be persistant, but the object is not, so if it isn't operating, you can't manage it.
* Current sytems do not allow things like dynamic channel mixing (detecting that a 6ch source is transmitting stereo and changing it to upmixed)
* Current systems do not have a enough useful persistant metadata to determine the most relevant sources/sinks (Plumbs)
* Current systems do not support network connections and locally distributed systems.
Example user story:

I am a user who wants to plug in 6 (5.1) channels of sound into an audio interface, and route it to my 5.1ch audio output. Both devices are already working audio devices.

Current systems either a) need extensive manual configuration or b) require you to connect each port one by one.

Plumb Jammer allows you to just jam those plumbs together!

## Scope
to be suitable for a home audio setup, small/midsize live audio setup, particularly focusing on streaming and podcasting, but surround sound is essential. Core features should not be introduced that are stereo only. (filters may be stereo only where explicitly stated)

* Does not show any devices unless actively configured (need to create a plumb)
* application connections have plumbs automatically created
* does not connect channels seperately (only devices)
* Simple connections and filter chains 
* Adding network endpoints on the fly.
* Plumbs can be single or bidirectional
* Plumbs are persistant
* Plumbs track activity
* Plumbs can have meters.


### Out of scope
It isn't within the core design goals to serve audiophiles, nor professional sound engineers. If it can, it should, but not if it compromises user experience.

Easy and obvious defaults and setup - completely flexible configuration when going further.


## Objects

* Plumb (audio source/sink/both)
* PlumbFilter 
* PlumbFilterChain
* PlumbGroup
* PlumbMeter
* PlumbRunner (Main object that does stuff)





## Plumb

### Core
**Properties**

* uuid
* Name
* frequency (if not all channels are the same is 0)
* bits (as above)
* channels
* layout - stereo,headphones,5.1 rear, 5.1 side, 2.1, 4.1, 7.1 (configurable)
* direction - sink/source/birectional
* group1
* supported_connections (eg vban, )


**functions**
* jam (item)
    connect to plumb. If both are bidirectional, this is the source
    if configured, may automatically create a network connection to complete the jam.
* filters(direction) returns a filterchain.
* filters(plumb) returns a tuple of three filterchains, src, src-dest, and dest.
* meter() - returns a list of meters connected to this plumb
* meter(PlumbMeter) - adds a meter to the plumb.

### Application Plumb
Application Sources:
Once they exist they will persist unless manually removed.
They can be configured to timeout (which will cause them to not be listed, but everything will be saved) after X inactivity.
They can be delisted (if inactive), and removed if required.
Can be assigned filters and routed the same as any other source. Filters will remain while the item is active, but will be removed if it times out.

* Communication sources - messenger, teams, zoom, webex,bluetooth phone, soft phone, whatever.
 * greylist - list of sources not to show by default (eg system sounds) 


### "Device" Plumb
Device types:
 * library of devices
  * Library of filter suggestions/settings for devices.

Sinks:
* have names
* have a channel layout
* Have types (which do hinting for auto filters)
* Have Custom sub types (user editable for auto filters)


### Network Plumb
* Network sources - VBAN, AVB?, other?
* Media sources - Spotify, Youtube.
* If they are a cast sink, they will connect 
* Can be Casting sinks:
 * Can be set to auto connect (if a signal is detected) or disconnected or connected. 
eg chromecast in, out, youtube music client, spotify client.
## PlumbGroup
A PlumbGroup is a selection of Plumbs that can natively route to each other. If You are only using it locally and everything is on pipewire, everything will be in one group. If you are using voicemeeter on windows connected to pipewire, you will have two groups. This can also be used for hinting by Curtain to roll up a group, depending on context.

Plumbs within a Plumbgroup have an order (two - one for in, one for out) -  this is managed by the wizard using rules.

## PlumbFilterChain
Chain of filters that apply to a plumb (or plumb pair) 
**properties**
* plumb  (either a plumb or plumb tuple)
* filters
**functions**
* jam(position,filter)
* move(filter,position)

## PlumbFilter
 * Entirely on demand. Created on the fly so you can have more/less. (could be pre-loaded for effeciency, but are used in a 1-for-1 way)
 * can be added to src chain, src-sink chain, or sink chain (chains are ordered)
  * if a filter is added to any of these chains, the settings are saved for that chain (which means auto filter changes are saved per 



**properties**
* filter_group
* controls - dict with controls and types. TBD
* custom_details - dict that details any custom metrics
* filter (the actual filter type)
**status**
* controlvalues
**metrics**
* latency
* CPU usage
* custom_metrics
**functions**
* jam
* move
* set_control



## PlumbMeter:
* Effectively a PlumbFilter, but not in line.

**properties**
* controls - dict with controls and types. TBD
* custom_details - dict that details any custom metrics
* meter (the actual meter type)
**status**
* controlvalues
**metrics**
* latency
* CPU usage
* custom_metrics
**functions**
* jam
* move
* set_control


## Wizard Rules
* Auto filters (if engaged, adds filter to src-sink filter chain at the end, tagged as auto, and removed if disconnected)
 * pre-defined auto filters - has a single filter to add, and default settings to use
  * 2ch auto adds a channel mapper filter to 4.1 if sent to 5.1 
  * 5.1ch auto maps to a spatial filter when connected to 2ch




