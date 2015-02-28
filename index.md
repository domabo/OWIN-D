[![OWIN-D](./owin-d.png)](http://owind.org)
## About

The purpose of the OWIN-D specification is to provide an abstraction from any IoT (Internet of Things) or Web Services for Devices protocol.

OWIN-D defines a standard framework for REST device servers written for io.js, Node.js and application/device logic. It works with any protocol such as COAP, WSDP, OIC iotivity, HomeKit, and can be a drop-in replacement for existing frameworks such as Connect/Express to re-use existing code.

OWIN-D is a superset of the OWIN-JS specifications for HTTP and COAP servers, supporting Node.JS enterprise-grade servers, browser-apps, and constained device implementations.

The goal of OWIN-D is to decouple transport and device logic and, by being an open standard, stimulate the open source ecosystem of Node.js web application/device development tools, without ties to any one framework or device protocol.

OWIN-D expands the REST philosophy to web servers, internet of things, etc.

## Reference Implementations

OWIN-D is the specification and contains no implementation source code.   However, reference implementations with fully functioning application and server stacks are only one click away:

* [limerun-device](http://limerun.com) - The OWIN-D reference device container for the reference OWIN-JS implementation for Javascript;  supports a selection of transport technologyies including CoAP (Constrained Application Protocol) iotivity, Homekit, and Web Services for Devices Profile.

* [nodekit.io](http://nodekit.io) - OWIN-JS implementations for OS/X and iOS desktop applications;  contains an embedded lightweight version of Node.js to run anywhere 


## Specifications
[OWIN-D Specification](./Specification.md)  (this repository)

[OWIN-JS Specification](http://owinjs.org)  (core REST technology on which OWIN-D extends)

## License
Creative Commons Attribution 3.0 Unported License