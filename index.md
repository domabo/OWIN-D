[![OWIN-D](./owin-d.png)](http://owind.org)
## About

This is the official repository of the OWIN-D (Open Web Interface for Networked Devices) Specification. 

The purpose of the OWIN-D specification is to provide a standard framework for developing and interacting with devices and accessories in the broad Interent of Things marketplace.     It is not yet another interoperability standard nor specificies a particular protocol (e.g., HomeKit, iotivity) or transport (e.g., HTTP, CoAP), but rather a simple abstraction to simplify development.

OWIN-D defines a standard framework for REST device containers that can be used with any protocol such as COAP, WSDP, OIC iotivity, Apple HomeKit, WSDP, and implementations based  on OWIN-D can even be a drop-in replacement for existing frameworks such as Connect/Express or ASP.NET V5 to re-use existing code.

OWIN-D is itself standards based, as an extension of the OWIN-JS specification, but specifically targeted for Internet of Things manufacturers and application developers.

There is no shortage of existing standards that are open, but even if they converge we still expect a fragmented marketplace of both open (e.g, iotivity, XMPP) and proprietary standards (e.g., HomeKit by Apple) that are likely to co-exist for some time under current business models.   

A device developer that wants to create a THING that can be used with one or more of these protocols can use OWIN-D to write the implementation once, but can rest assured that the underlying protocol is supported and even certified by the existing standards body.

## Reference Implementations

OWIN-D is the specification and contains no implementation source code.   However, reference implementations with fully functioning application and server stacks are only one click away:

* [limerun-device](http://limerun.com) - The OWIN-D reference device container for the reference OWIN-JS implementation for Javascript;  supports a selection of transport technologyies including CoAP (Constrained Application Protocol) iotivity, Homekit, and Web Services for Devices Profile.

* [nodekit.io](http://nodekit.io) - OWIN-JS implementations for OS/X and iOS desktop applications;  contains an embedded lightweight version of Node.js to run anywhere 


## Specifications
[OWIN-D Specification](./Specification.md)  (this repository)

[OWIN-JS Specification](http://owinjs.org)  (core REST framework which OWIN-D extends)

## License
Creative Commons Attribution 3.0 Unported License