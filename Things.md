[![OWIN-D](./owin-d.png)](http://owind.org)
# Things

* **Ecosystem** &mdash; A collection of things that are addressable to each other (e.g., for discovery, transfer operatons etc.)

* **Thing** &mdash; Every component in OWIN-D is a thing that can be connected to each other or the Internet.  A thing can be a Home, a Room, a Device, or even a Service within a device (for example, a garage door opener might have a door-opener service, a light-bulb service, and a firmware update service).

* **Container** &mdash; Every device is hosted in a container.  A container can contain one or more devices.   A container is generally the addressable end-point for communicating with its child devices.   For example a Hue Bridge is the container for all its connected light bulb devices.

* **Device** (or Accessory) &mdash; A device is an accessory or technology that a human can interact with or has interest in. While a device  generally represents something in the real world, it can be logical (say a program running in a container on a Raspberry Pi that connects to an Internet Weather Service) or physical (such as a Hue Light bulb)

* **Service** &mdash; A service includes user-readable or controllable functions, like a light, and machine-functions like a firmware update service.   A single device may have more than one user-controllable service. For example, a garage door opener has a door-opener service, and a light-bulb service.

* **Resource** (or Characteristic) &mdash; A resource is a characteristic of a service; at any given time, a resource will have one or more URIs to access it (e.g., `coap://containerhost/devicename/servicename/resourcename`).  Unlike the URN these are not guaranteed to be persistent, even across reboots


## Extensions

The full power of the OWIN-D specification comes from its extensions and a broad array of middleware. 

### Things Enabled by a Home Controller

* **Home** &mdash; A home is a geographically-colocated grouping of devices usually used by one family resource unit or organization.  Sometimes known as a house or a a building.  An application called a home manager can manage multiple homes (e.g., house and guest cottage, primary and vacation home, etc.)

* **Room** &mdash; A room is a geographical subdivision of a home, usually corresponding to a physical area.    Can include hallways, cupboards, etc.


### Things Enabled by a Zone Controller


* **Zone** &mdash; A zone is an optional grouping of Rooms in a Home, and/or a collection of Accessories that are related in some way (location, use, etc.).  Examples of zones include "outside lights", "upstairs rooms", "emergency lighting".  A single device can be in multiple zones.

* **Service Group** &mdash; A service group is a logical collection of services on one or more devices

### Things Enabled by a Scene Controller


* **Scene** &mdash; A scene is a target collection characteristic operations applied to a service group (e.g., lock doors, dusk, movie time, etc.)

* **Trigger** &mdash; A trigger that plays a particular scene or zone on/off on a given schedule (every, date, time, delay, repeat)


## Properties of Things

Every OWIN-D THING includes the following properties:

* URN &mdash; a persistent uniform resource name in the format urn:UUID.  It MUST be persistent across reboots
* Class &mdash; the class to which the thing belongs (e.g., "light");  can be a custom URN
* Interface &mdash; a generic interface used to interact with the thing
* Manufacture Name
* Friendly name
* Manufacturer
* Model
* Serial Number
* Password
* Setup code (password)


Each resource includes the following properties

* URN &mdash; a persistent uniform resource name in the format urn:UUID
* Type (e.g., "brightness")
* Manufacturer description
* Value
* Value format
* Value units
* Value interface (readable, writable, eventable)
* Value max, min and step values
* Value precision, maximum length

At any given time, a resource will have one or more URIs to access it (e.g., coap://containerhost/devicename/servicename/resourcename ).  Unlike the URN these are not guaranteed to be persistent, even across reboots.



