[![OWIN-D](./owin-d.png)](http://owind.org)
# OWIN-D Specification

## About

The purpose of the OWIN-D specification is to provide an abstraction from any IoT (Internet of Things) or Web Services for Devices protocol.

OWIN-D defines a standard framework for REST device servers written for io.js, Node.js and application/device logic. It works with any protocol such as COAP, WSDP, OIC iotivity, HomeKit, and can be a drop-in replacement for existing frameworks such as Connect/Express to re-use existing code.

OWIN-D is a superset of the OWIN-JS specifications for HTTP and COAP servers, supporting Node.JS enterprise-grade servers, browser-apps, and constained device implementations.

The goal of OWIN-D is to decouple transport and device logic and, by being an open standard, stimulate the open source ecosystem of Node.js web application/device development tools, without ties to any one framework or device protocol.

OWIN-D expands the REST philosophy to web servers, internet of things, etc.

## OWIN-D Things

### Thing

Every component in OWIN-D is a thing that can be connected to the Internet.  A thing can be a Home, a Room, a Device, or even a Service within a device (for example, a garage door opener might have a door-opener service, a light-bulb service, and a firmware update service).

Every Thing has the following attributes:

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

### Things Enabled by a Home Controller

#### Home

A home is a geographically-colocated grouping of devices usually used by one family resource unit or organization.  Sometimes known as a house or a a building.  

An application called a home manager can manage multiple homes.

#### Room

A room is a geographical subdivision of a home, usually corresponding to a physical area.    Can include hallways, cupboards, etc.


### Things Enabled by a Zone Controller

#### Zone

A zone is an optional grouping of Rooms in a Home, and/or a collection of Accessories that are related in some way (location, use, etc.).  Examples of zones include "outside lights", "upstairs rooms", "emergency lighting".

A single device can be in multiple zones.

### Things Enabled by a Scene Controller

#### Service Group

A service group is a logical collection of services on one or more devices

#### Scene (action set)

A scene is a target collection characteristic operations applied to a service group (e.g., lock doors, dusk, movie time, etc.)

### Things Enabled by a Timer Controller

#### Trigger

A trigger that plays a particular scene or zone on/off on a given schedule (every, date, time, delay, repeat)


### Things native to the OWIN-D spec

### Container

Every device is hosted in a container.  A container can contain one or more devices.   A container is generally the addressable end-point for communicating with its child devices.   For example a Hue Bridge is the container for all its connected light bulb devices.

### Device (Accessory)

A device is an accessory or technology that a human can interact with or has interest in. 

While a device  generally represents something in the real world, it can be logical (say a program running in a container on a Raspberry Pi that connects to an Internet Weather Service) or physical (such as a Hue Light bulb)

### Service

A service includes user-readable or controllable functions, like a light, and machine-functions like a firmware update service.

A single device may have more than one user-controllable service. For example, a garage door opener has a door-opener service, and a light-bulb service.


### Resource (Characteristic)

A resource is a characteristic of a service;  each service can 

Each resource has the following properties

* URN &mdash; a persistent uniform resource name in the format urn:UUID
* type (e.g., "brightness")
* manufacturer description
* format
* units
* interface (readable, writable, eventable)
* max, min and step values
* precision, maximum length

At any given time, a resource will have one or more URIs to access it (e.g., coap://containerhost/devicename/servicename/resourcename ).  Unlike the URN these are not guaranteed to be persistent, even across reboots


### Operation

An operation that can be applied to a resource.

Examples include "GET", "SET" or "PLAY"







