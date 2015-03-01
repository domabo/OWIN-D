[![OWIN-D](./owin-d.png)](http://owind.org)
# OWIN-D Specification

## About

The purpose of the OWIN-D specification is to provide a standard framework for developing and interacting with devices and accessories in the broad Interent of Things marketplace.     It is not yet another interoperability standard nor specificies a particular protocol (e.g., HomeKit, iotivity) or transport (e.g., HTTP, CoAP), but rather a simple abstraction to simplify development.

OWIN-D is just a specification, not an implementation or consumer app, but reference implementations already exist and some are linked at the end of this document.

### Standards-Based


OWIN-D defines a standard framework for REST device containers that can be used with any protocol such as COAP, WSDP, OIC iotivity, Apple HomeKit, WSDP, and implementations based  on OWIN-D can even be a drop-in replacement for existing frameworks such as Connect/Express or ASP.NET V5 to re-use existing code.

OWIN-D is itself standards based, as an extension of the OWIN-JS specification, but specifically targeted for Internet of Things manufacturers and application developers.

### Does Not Replace Existing Standards

There is no shortage of existing standards that are open, but even if they converge we still expect a fragmented marketplace of both open (e.g, iotivity, XMPP) and proprietary standards (e.g., HomeKit by Apple) that are likely to co-exist for some time under current business models.   

A device developer that wants to create a THING that can be used with one or more of these protocols can use OWIN-D to write the implementation once, but can rest assured that the underlying protocol is supported and even certified by the existing standards body.

### Loosely Coupled  

The goal of OWIN-D is to decouple transport and device logic and, by being a free open-source standard (under Creative Commons), stimulate the open source ecosystem of IoT device development tools, without ties to any one framework or device protocols, while at the same time being used in commercial applications without restriction.

### Simple, Mature, REST Philosophy  

OWIN-D expands the well-understood and mature REST philosophy from web servers to Internet of Things, etc., and thus removes most of the complexity traditionally inherent in writing applications for devices.

In particuarl, OWIN-D is defined in terms of a delegate structure and extensible property dictionaries that translate to any programming language. There is no assembly or library required. Implementing either the server or client side of the OWIN-D spec does not introduce a dependency to a project.

### OWIN-D, OWIN-JS, and limerun 

We recommend reviewing the [OWIN-JS Specification](http://owinjs.org) and [limerun framework](http://limerun.com) in conjunction with this OWIN-D specification.







