# Plumb Jammer

## What is it.

Plumb Jammer is a Library that sits over the top of pipewire and wire plumber that simplifies and abstracts away all the ports and focuses on virtual devices (Plumbs) that can be plugged (jammed) into each other. Filters are able to be defined for any Plumb, as in or out (which applies to all connections), and for pairs of Plumbs. Plumbs are persistant (even if their backing object isn't present), so any application that is used can now be configured and routed even if it's not running.

### Curtain Manager
Plumb Jammer is a relatively simple library with no front end, because it's intended to be used with [Curtain Manager](curtain.md) and Curtain (and [Surface Presser](surfacepresser.md)). This provides the advanced rulesets, as well as a nice user interface to both configure and jam plumbs. 

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
* PlumbMeter
* PlumbRunner (Main object that does stuff)
* 
PlumbSource.jam(PlumbSink)
PlumbSource.filters().jam(newfilter)
PlumbSource.filters(PlumbSink).jam(newfilter) is the same as PlumbSink.filters(PlumbSource).jam(newfilter)
PlumbJammer.Plumb()



## Plumb

### Core


Other options:
* Latency alerts:
 * specify what level of latency is acceptable.

Sources:
* Network sources - VBAN, AVB?, other?
* Media sources - Spotify, Youtube.
* Communication sources - messenger, teams, zoom, webex,bluetooth phone, soft phone, whatever.


### Application Plumb
Application Sources:
Once they exist they will persist unless manually removed.
They can be configured to timeout (which will cause them to not be listed, but everything will be saved) after X inactivity.
They can be delisted (if inactive), and removed if required.
Can be assigned filters and routed the same as any other source. Filters will remain while the item is active, but will be removed if it times out.


### "Device" Plumb

Sinks:
* Are ordered - this is how they display on screen and for devices.
* have names
* have a channel layout
* If they are a cast sink, they will connect 
* Can be Casting sinks:
 * Can be set to auto connect (if a signal is detected) or disconnected or connected. 
* Have types (which do hinting for auto filters)
* Have Custom sub types (user editable for auto filters)


### Network Plumb

Device types:
 * library of devices
  * Library of filter suggestions/settings for devices.
  


## PlumbFilter
* Auto filters (if engaged, adds filter to src-sink filter chain at the end, tagged as auto, and removed if disconnected)
 * pre-defined auto filters - has a single filter to add, and default settings to use
  * 2ch auto adds a channel mapper filter to 4.1 if sent to 5.1 
  * 5.1ch auto maps to a spatial filter when connected to 2ch
 * Entirely on demand. Created on the fly so you can have more/less. (could be pre-loaded for effeciency, but are used in a 1-for-1 way)
 * can be added to src chain, src-sink chain, or sink chain (chains are ordered)
  * if a filter is added to any of these chains, the settings are saved for that chain (which means auto filter changes are saved per 
 * greylist - list of sources not to show by default (eg system sounds) 
 * if communication source active, mute/pause all media in the group with that source.


PlumbMeter:
* When viewing from a [src/sink] perspective, the total latency to/from an activated endpoint will be displayed.
 * Possibly latency on all filters?
* CPU/RAM usage
 * Process list (of just filters and source/sinks)
* Sync Errors?


Displays:
 




Pi4

I/O from the projectmix - headphones.


piperouter
- overlay API on pipewire, allowing for console mixer type functions - plugging devices into each other, filter chains of predefined filters and such.
exposed via rest, 



sink/src info

All Plumbs:
Arbitrary tags and values.

Baskets (and Squishes - sub baskets)
Dynamic Baskets
- Rules

Controllers have modes - defines the Pressing and Squish Baskets.


PLumb Sink (optional Context: Pressing Basket -> selected Plumb Source)
 - standard actions:
  - solo (disconnect all other sinks from source)
  - mute (mute - if in context mute src-sink level control)
  - level (change level - if in context, insert a level control filter src-sink and adjust that)
  - sel (un/link src-sink toggle if in context)
  - rec (Cycle through filters and show controls?)
Plumb Source (optional Context: Plumb Sink) 


Plumb Jammer and Surface Presser *need* curtain, and are native curtain services. Other services are integrations of pre-existing services

Curtain Service (message library, standard message formats, fast messaging, management framework, etc)

Curtain API/library
 - Doesn't *need* Ballon , can be used simply for in process message management.



-> Client integration.
Surface Presser (MIDI Interface)
Plumb Jammer (pipewire overlay,audio management)
Home Assistant.
VBAN control (also integrates with Plumb Jammer)
dbus interface -> bluetooth/KDE/
 
Plumb Jammer
 -> VBAN
 -> 
 -> streaming
  -> generic streaming (playlist)
  -> spotify
  -> cast target
  -> youtube music
  
 
G 




