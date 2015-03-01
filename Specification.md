[![OWIN-D](./owin-d.png)](http://owind.org)
#Specification v1.0 RC 
* Title: Open Web Interface for Networked Devices (OWIN-D)
* Author : OWIN-JS working group
* Copyright : OWIN-JS contributors, Domabo 2015
* License : [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/us/)

## Contents
  
1\. [Overview][1]

2\. [Definitions][200]

2.1. [OWIN-D Things][2]

2.2. [OWIN-D Extensions][3]

2.3. [OWIN-D Core Functions][4] 

2.3. [OWIN-D Containers][5]

3\. [Application Execution][6] 

3.1. [Application Delegate][7]

3.2. [Environment][8]

4\. [OWIN-D Context Dictionary][9]

4.1. [OWIN-D Device Context][10]

4.2. [Service Context Properties][11]

4.3. [Resource Context Properties][12]

4.3.1. [Optional Resource Format Context Properties][13]

5\. [OWIN-D Capabilities][14]

5.1. [OWIN-D Support Dictionary (Server)][15]

5.2. [OWIN-D Support Dictionary (Client)][16]

5.3. [OWIN-D Capabilities API Reference][17]

6\. [Error Handling][18]

6.1. [Application Errors][19]

6.2. [Server Errors][20]

7\. [Versioning][21]

8\. [Extensions][22]

9\. [Real World Usage][24]

## 1\. Overview

The purpose of the Open Web Interface for Networked Devices (OWIN-D) specification is to provide a standard framework for developing and interacting with devices and accessories in the broad Interent of Things marketplace.     It is not yet another interoperability standard nor specificies a particular protocol (e.g., HomeKit, iotivity) or transport (e.g., HTTP, CoAP), but rather a simple abstraction to simplify development.

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

In this document, the ECMAScript, Javascript, Node.js `function` and C# `Action`/`Func` syntax is used to notate some delegate structures.   However, the delegate structure could be equivalently represented with other native functions, CLR interfaces, or named delegates. This is by design; when implementing OWIN-D, choose a delegate representation that works for you and your stack.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119][25].

### OWIN-D, OWIN-JS, and limerun 

We recommend reviewing the [OWIN-JS Specification](http://owinjs.org) and [limerun framework](http://limerun.com) in conjunction with this OWIN-D specification.

## 2\. Definitions 
### 2.1. OWIN-D Things

* **Ecosystem** &mdash; A collection of things that are addressable to each other (e.g., for discovery, transfer operatons etc.)

* **Thing** &mdash; Every component in OWIN-D is a thing that can be connected to each other or the Internet.  A thing can be a Home, a Room, a Device, or even a Service within a device (for example, a garage door opener might have a door-opener service, a light-bulb service, and a firmware update service).

* **Container** &mdash; Every device is hosted in a container.  A container can contain one or more devices.   A container is generally the addressable end-point for communicating with its child devices.   For example a Hue Bridge is the container for all its connected light bulb devices.

* **Device** (or Accessory) &mdash; A device is an accessory or technology that a human can interact with or has interest in. While a device  generally represents something in the real world, it can be logical (say a program running in a container on a Raspberry Pi that connects to an Internet Weather Service) or physical (such as a Hue Light bulb)

* **Service** &mdash; A service includes user-readable or controllable functions, like a light, and machine-functions like a firmware update service.   A single device may have more than one user-controllable service. For example, a garage door opener has a door-opener service, and a light-bulb service.

* **Resource** (or Characteristic) &mdash; A resource is a characteristic of a service; at any given time, a resource will have one or more URIs to access it (e.g., `coap://containerhost/devicename/servicename/resourcename`).  Unlike the URN these are not guaranteed to be persistent, even across reboots


### 2.2. OWIN-D Extensions

The full power of the OWIN-JS specification comes from its extensions and a broad array of middleware, and OWIN-D is no different.  In addition to the above OWIN-D definitions for this specification, standard OWIN-D extensions also define:

* **Home** &mdash; A home is a geographically-colocated grouping of devices usually used by one family resource unit or organization.  Sometimes known as a house or a a building.  An application called a home manager can manage multiple homes (e.g., house and guest cottage, primary and vacation home, etc.)

* **Room** &mdash; A room is a geographical subdivision of a home, usually corresponding to a physical area.    Can include hallways, cupboards, etc.

* **Zone** &mdash; A zone is an optional grouping of Rooms in a Home, and/or a collection of Accessories that are related in some way (location, use, etc.).  Examples of zones include "outside lights", "upstairs rooms", "emergency lighting".  A single device can be in multiple zones.

* **Service Group** &mdash; A service group is a logical collection of services on one or more devices

* **Scene** &mdash; A scene is a target collection characteristic operations applied to a service group (e.g., lock doors, dusk, movie time, etc.)

* **Trigger** &mdash; A trigger that plays a particular scene or zone on/off on a given schedule (every, date, time, delay, repeat)

Not all OWIN-D implementations will implement these extensions, and a DEVICE MAY ONLY assume their capability when indicated in the Server.Capabilities dictionary

### 2.3. OWIN-D Core Functions 

THe OWIN-D specification provides for a number of common functions that apply to nearly all IoT (Internet of Things) or device networks, regardless of transport protocol (IP, bluetooth, radio wave, etc.)

* **Discovery** &mdash; A set of coordinated peer and/or registry functions that allow ecosystem things to find and connect to each other.  

* **Transfer** &mdash; An operation that is sent to a RESOURCE on a target DEVICE within the ecosystem. Examples include "GET", "SET" or "PLAY".  It MAY return a response.

* **Eventing** &mdash; The ability for a subscriber to receive a periodic stream of observations from a publisher

These core functions MAY abstract and include underlying functions such as **meta data exchange**, **pairing**, **acknowledgments**, **confirmable send**, **policy**, **security**, etc.   Equally these functions SHOULD be available as explicit extensions in the environment dictionary.

### 2.3. OWIN-D Containers

A CONTAINER is just a server that advertises and responds to requests for multiple devices.  All OWIN-D servers are CONTAINER, they MAY contain one or more devices.


## 3\. Application Execution 

As an extension to OWIN-JS, the OWIN-D specification follows the execution model of OWIN-JS.   In summary, an OWIN-D server invokes an application (providing as arguments an environment dictionary with request and response headers and bodies); an application either populates a response or indicates an error.  

On startup, an OWIN-D server provides the environment dictionary (which is also provided on each request) which allows for device registration for each DEVICE, SERVICE and RESOURCE hosted by by the application (CONTAINER).

### 3.1. Application Delegate

The primary interface in OWIN-JS and OWIN-D is called the _application delegate_ or _AppFunc_. An application delegate takes the Dictionary environment and returns a Promise or a Task when it has finished processing.

    
#### OWIN-JS Node.js AppFunc (returns a Promise/A)

    var myAppFuncPromise = function() {...};

where `this` is set to the Dictionary environment and `myAppFuncPromise` is a Promise/A promise that can be chained with     `myAppFuncPromise.then(... , ... )` etc.
    
#### OWIN-JS .NET AppFunc (returns a Task)

    using AppFunc = Func<
        IDictionary<string, object>, // Environment
        Task>; // Done


> The application MUST eventually complete the returned _task/promise_, or throw an exception.

### 3.2. Environment

The Environment object stores information about the request, the response, and any relevant server state.  The server is responsible for providing body streams and header collections for both the request and response in the initial call. The application then populates the appropriate fields with response data, writes the response body, and returns when done.  

* The environment object MUST be non-null, mutable and MUST contain the keys listed as required in the [OWIN-JS Specification](http://owinjs.com).  Any device specific information SHOULD be added using the keys in the tables later in this OWIN-D specification

* Keys MUST be compared using StringComparer.Ordinal.

* The values associated with the keys MUST be non-null, unless otherwise specified

* The implementation MAY provide aliases that are convenient to access in the selected programming language chosen (i.e., ECMAScript/JavaScript, C#) to avoid `context["owin.Key"]` type accessors in favor of `this.owin.Key` (for intellitype, strong typing, capitalization conventions, separation of `request` and `response` objects, etc.).  

* If a server does not implement alias names, middleware such as [limerun](http://github.com/limerun/core) MAY be used to add such alias names.  

* Periods in **OWIN-D Key Names** are considered part of the single string and therefore require quotes for access in most C-style and ECMAScript languages (e.g., `var serial = context["owind.SerialNumber"];`).

* Implementations of OWIN-D servers and/or middleware harnesses MAY omit the context variable as an explicit parameter for applications and middleware functions and instead set the base language's context object (e.g., `this` in ECMAScript/Javascript).

* The environment dictionary SHOULD allow additional prototype methods to be added to its prototype object, to facilitate alias implementations that are  defined once per server instance

## 4\. OWIN-D Context Dictionary

## 4.1. OWIN-D Device Context

### Device Model Properties

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Manufacturer** | Name of the manufacturer of the DEVICE. It MUST have fewer than 256 Unicode characters
No | **owind.ManufacturerUrl** | URL to a Web site for the manufacturer of the DEVICE. It MUST have fewer than 2,048 octets.
No | **owind.ModelName** | User-friendly name for this model of device chosen by the manufacturer. It MUST have fewer than 256 Unicode characters
No | **owind.ModelNumber** | Model number for this model of DEVICE. It MUST have fewer than 256 Unicode characters.
No | **owind.ModelUrl** | URL to a Web site for this model of DEVICE. It MUST have fewer than 2,048 octets.
No | **owind.PresentationUrl** | URL to a presentation resource for this DEVICE. It MAY be relative to the transport address over which metadata was retrieved, and MUST have fewer than 2,048 octets.  If PresentationUrl is specified, the DEVICE MAY provide the resource in multiple formats, but MUST at least provide an HTML page.  CLIENTs and DEVICEs MAY use transport content negotiation [e.g., HTTP/1.1, COAP/1.0] to determine the format and content of the presentation resource.  DEVICEs that use a relative URL MAY use Transport Redirection (e.g., 3xx codes for HTTP/1.1) to direct CLIENTs to a dedicated content server running on another port.


### Device Instance Properties

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.DeviceId** | Persistent identifier for this DEVICE, typically the MAC address;  the DeviceId MAY be stable for as long as a DEVICE is in a given ECOSYSTEM
Yes | **owind.Urn** | Unique Resource Name for this device, often used for validation on pairing and for resolve requests
Yes | **owind.SetupCode** | Password code used during connection pairing
Yes | **owind.FriendlyName** | User-friendly name for this DEVICE. It MUST have fewer than 256 Unicode characters
Yes | **owind.SerialNumber** | Manufacturer-assigned serial number for this DEVICE. It MUST have fewer than 256 Unicode characters.
No | **owind.FirmwareVersion** | Firmware version for this DEVICE. It MUST have fewer than 256 Unicode characters.
No | **owind.Services** | Array of SERVICE property dictionaries


Example usage:
``` js
context["owind.Manufacturer"] = "Domabo";
context["owind.ManufacturerUrl"] = "http://domabo.com";
context["owind.ModelName"] = "Domabot X500";
context["owind.ModelNumber"] = "D-X500";
context["owind.ModelUrl"] = "http://domabo.com/products/domabot/x500";
context["owind.PresentationUrl"] = "/img/img.jpg";
context["owind.DeviceId"] = "1A:2B:3C:4D:5E:FF";
context["owind.Urn"] = "urn:af6aacb6-17e0-45aa-9fc0-c4090f9c1f53";
context["owind.SetupCode"] = "098-45-211";
context["owind.FriendlyName"] = "LimeRun Test OWIN-D Server";
context["owind.SerialNumber"] = "1234567890";
context["owind.FirmwareVersion"] = "0.85A";
``` 

## 4.2. Service Context Properties

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Urn** | Unique Resource Name of the service
Yes | **owind.ResourcePath** | The OWIN-JS request path. The path MUST be relative to the "root" of the application CONTAINER, and for a SERVICE or DEVICE MUST be the base onto which [well-known](http://tools.ietf.org/html/rfc5785) sub-paths (e.g., "/oc/core" or ".well-known/core") are appended;  not necesssarily persistent across reboots of the CONTAINER but SHOULD NOT change due to arbitary network reconfigurations
Yes | **owind.ServiceType** | The OWIN-D service type or custom type URN
Yes | **owind.FriendlyName** | User-friendly name for this SERVICE. It MUST have fewer than 256 Unicode characters
No | **owind.Resources** | Array of RESOURCE property dictionaries
No | **owind.Parent** | Reference to parent DEVICE properties dictionary

## 4.3. Resource Context Properties

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Urn** | Unique Resource Name of the service
Yes | **owind.ResourcePath** | The OWIN-JS request path. The path MUST be relative to the "root" of the application CONTAINER, and for a SERVICE or DEVICE MUST be the base onto which [well-known](http://tools.ietf.org/html/rfc5785) sub-paths (e.g., "/oc/core" or ".well-known/core") are appended;  not necesssarily persistent across reboots of the CONTAINER but SHOULD NOT change due to arbitary network reconfigurations
Yes | **owind.ResourceType** | The OWIN-D resource type or custom type URN
Yes | **owind.FriendlyName** | The user-friendly name for this RESOURCE. It MUST have fewer than 256 Unicode characters
Yes | **owind.ResourceInterface** | The OWIN-D interface type (e.g., binary switch)
No | **owind.Parent** | Reference to parent SERVICE properties dictionary

### 4.3.1. Optional Resource Format Context Properties
Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
No | **owind.ResourceFormat** | int, float or string, etc.
No | **owind.ResourceValueMin** | The minimum value for the resource value 
No | **owind.ResourceValueMax** | The maximum value for the resource value 
No | **owind.ResourceValueStep** | The increment value for the resource value 
No | **owind.ResourceValuePrecision** | The precision of the resource value 
No | **owind.ResourceValueMaxLength** | The maximum length of the resource value 

Example:

``` js
serviceProperties["owind.ResourcePath"] =  "/device1/lightservice" 
brightnessProperties["owind.RequestPath"] = "http://127.0.0.1:12001/device1/lightservice/brightness";
``` 


## 5\. OWIN-D Capabilities

The OWIN-JS application startup environment dictionary and each request will contain a ["server.Capabilities"] object which for OWIN-D incldues

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Version** | Current version of OWIN-D supported (e.g., "1.0")
Yes | **owind.Support** | OWIN-D Support Dictionary below 

### 5.1. OWIN-D Support Dictionary (Server)

OWIN-D Function Name | Value Description
------------- | -------------------------------------
**owind.Register** | Function that registers a DEVICE, SERVICE or RESOURCE and starts advertising it on the underlying transport server.  Advertising includes sending HELLO messages, and responding to discovery probe and resolve messages.   DEVICE definition MAY contain child SERVICES and RESOURCES, or these MAY be registered individually.  If previously registered, this function updates the existing DEVICE, SERVICE or RESOURCE definition.
**owind.Unregister** | Function that stops advertising a registered device.


### 5.2. OWIN-D Support Dictionary (Client)

OWIN-D Function Name | Value Description
------------- | -------------------------------------
**owind.DiscoveryProbe** | Function that probes for a DEVICE in the local ECOSYSTEM.  Calls back provided OWIN-JS AppFunc for each device found. 
**owind.DiscoveryResolve** | Function that resolves the transport location for a given DEVICE by unique identifier in the local ECOSYSTEM.  
**owind.CreateTransferRequest** | Function that creates an OWIN-D context dictionary for an outgoing request to a given device.  See multicastTransfer extension for transports that support requests to multiple devices.  The returned context includes a full dictionary including `owin.RequestBody` stream which is used to complete the request.

### 5.3. OWIN-D Capabilities API Reference

#### \["owind.Register"\](context)
Registers a DEVICE, SERVICE or RESOURCE for advertising on the underlying transport server.  

Advertising includes sending HELLO messages, and responding to discovery probe and resolve messages.   DEVICE definition MAY contain child SERVICES and RESOURCES, or these MAY be registered individually.  If previously registered, this function updates the existing DEVICE, SERVICE or RESOURCE definition. 

| Param | Type | Description |
| --- | --- | --- |
| context | OWIN-D dictionary | Context dictionary for the DEVICE, SERVICE, or RESOURCE being registered

**Example**  

``` js
function middleware()
{
    var context {
       "owind.Manufacturer" : "Domabo"
	  , "owind.ManufacturerUrl" : "http://domabo.com"
	  , "owind.ModelName" : "Domabot X500"
	  , "owind.ModelNumber" : ""D-X500"
	  , "owind.ModelUrl" : "http://domabo.com/products/domabot/x500"
	  , "owind.PresentationUrl" : "/img/img.jpg"
	  , "owind.DeviceId" : "1A:2B:3C:4D:5E:FF"
	  , "owind.DeviceUrn" : "urn:af6aacb6-17e0-45aa-9fc0-c4090f9c1f53"
	  , "owind.SetupCode" : "098-45-211"
	  , "owind.FriendlyName" : "LimeRun Test OWIN-D Server"
	  , "owind.SerialNumber" : "1234567890"
	  , "owind.FirmwareVersion" : "0.85A"
	  };
	  var owind = this["server.Capabilities"]["owind.Support"];
	  owind["owind.Register"](context);
}
```


#### \["owind.Unregister"](urn)
Registers a DEVICE, SERVICE or RESOURCE for advertising on the underlying transport server.  

Advertising includes sending HELLO messages, and responding to discovery probe and resolve messages.   DEVICE definition MAY contain child SERVICES and RESOURCES, or these MAY be registered individually.  If previously registered, this function updates the existing DEVICE, SERVICE or RESOURCE definition. 

| Param | Type | Description |
| --- | --- | --- |
| urn | string | The owind.DeviceUrn of the device being unregistered

Returns promise that fulfills when unregistration is complete (e.g., discovery BYEs have been sent).

``` js
function middleware(properties)
{
	this._id = "urn:af6aacb6-17e0-45aa-9fc0-c4090f9c1f53";
	this_owind = properties["server.Capabilities"]["owind.Support"];
}    
:
function middleware_close()
{ 
   return this._owind["owind.Unregister"](this._id);
}
```

#### \["owind.DiscoveryProbe"](context[, appFunc])
Function that probes for a DEVICE in the local ECOSYSTEM.  Calls back provided OWIN-JS AppFunc for each device found. 

| Param | Type | Description |
| --- | --- | --- |
| context | OWIN-D dictionary | Context dictionary containing the filter information of the device being probed (e.g., owind.ServiceType)
| appFunc | OWIN-JS function(context) | optional function that is called for each device found;  the first device is also returned with the return parameter

returns promise that fulfills with first device context or timeout error

#### \["owind.DiscoveryResolve"](urn)
Function that resolves for a given DEVICE urn in the local ECOSYSTEM.  Calls back provided OWIN-JS AppFunc for each device found. 

| Param | Type | Description |
| --- | --- | --- |
| urn | string | The owind.DeviceUrn of the device being sought

returns promise that fulfills with the device context or timeout error

#### \["owind.CreateTransferRequest"](urn)  *or*
#### \["owind.CreateTransferRequest"](context)
Function that creates an OWIN-D context dictionary for an outgoing request to a given device.  The returned context includes a full dictionary including `owin.RequestBody` stream which is used to complete the request and `owin.ResponseBody` stream which is used to process and track (`.on("response")`)the response.

| Param | Type | Description |
| --- | --- | --- |
| urn | string | The owind.DeviceUrn of the target device;  used to lookup within local discovery cache or by discovery resolve the transport destination
| context | OWIN-D dictionary | The full context (which includes transport details) of the target device

**EXACTLY one of urn or context MUST be specified**

returns new context with OWIN-JS/OWIN-D request/response dictionary.   Use `["owin.RequestBody"].end()` to send the request and `["owin.ResponseBody"].on("response")` to track the response.

## 6. Error Handling

While there are standard exceptions such as Argument Exceptions and IO Exceptions that may be expected in normal request processing scenarios, handling only such exceptions is insufficient when building a robust server or application. If a server wishes to be robust it SHOULD consistently address all exception types thrown or returned from the application delegate or body delegate. The handling mechanism (e.g. logging, crashing and restarting, swallowing, etc.) is up to the server and host process.

### 6.1. Application Errors

An application may generate an exception in the following places:

  * Thrown from an invocation of the application delegate.
  * Provided as the result of the application delegate Task/Promise

An application SHOULD attempt to trap its own internal errors and generate an appropriate (e.g., 500 for HTTP, 5.00 for CoAP) response rather than propagating an exception up to the server.

After an application provides a response, the server SHOULD wait to receive at least one write from the response Stream before writing the response headers to the underlying transport. In this way, if instead of a write to the Stream the server gets an exception from the application delegate Task, the server will still be able to generate a 500-level response. If the server gets a write to the Stream first, it can safely assume that the application has caught as many of its internal errors as possible; the server can begin sending the response. If an exception is subsequently received, the server MAY handle it as it sees fit (e.g. logging, write a textual description of the error to the underlying transport, and/or close the connection).

### 6.2. Server Errors

When a server encounters errors during a request’s lifetime it SHOULD signal the CancellationToken it provided in `owin.CallCancelled`. The server MAY then take any necessary actions to terminate the request, but it SHOULD be tolerant of completion delays of the application delegate.

## 7\. Versioning

Future updates to this standard may contain breaking changes (e.g. signature changes, key additions or modifications, etc.) or non-breaking additions. While addressing specific changes is the responsibility of later versions of the standard, here are initial guidelines for expected changes:

* This standard uses Semantic Versioning as described at  (e.g. Major.Minor.Patch).

* Breaking changes to the API signatures or existing keys will require incrementing the major version number (e.g. OWIN-D 2.0)

* Adding new keys or delegates in a backwards compatible way only requires incrementing the minor version number (e.g. OWIN-D 1.1).

* Making corrections and clarifications to the document alone only requires incrementing the patch version number and last modified date (e.g. OWIN-D 1.0.1).

* The `"owind.Version"` key in the startup Properties and request Environment dictionaries indicates the latest version of the standard implemented by the server and may be used to dynamically adjust behaviors of applications.  Major and Minor versions are kept consistent on OWIN-D to match OWIN-JS as far as practical.

* All implementers SHOULD clearly document the full version number(s) of the OWIN-D standard they support.

* The keys listed in Extensions are strictly optional. Additions may be made there without directly affecting the OWIN-D standard or version number.

## 8. Extensions

None defined at this time.  Extensions under consideration include Multicast Transfer, Security, Pairing, Homekit, Nodekit.io, etc.

## 9. Real World Usage

| Project | Description |
| --------- | ----------- |
| [lime-device](https://github.com/limerun/lime-device/master/README.md)| Reference implementation of OWIN-D that runs on the reference OWIN-JS limerun framework or Node javascript servers and clients|

   [1]: #1-overview
   [200]: #2-Definitions
   [2]: #21-owin-d-things
   [3]: #22-owin-d-extensions
   [4]: #23-owin-d-core-functions
   [5]: #24-owin-d-containers
   [6]: #3-application-execution
   [7]: #31-application-delegate
   [8]: #32-environment
   [9]: #4-owin-d-context-dictionary
   [10]: #41-owin-d-device-context
   [11]: #42-serice-context-properties
   [12]: #43-resource-context-properties
   [13]: #431-optional-resource-format-context-properties
   [14]: #5-owin-d-capabilities
   [15]: #51-owin-d-support-dictionary-(server)
   [16]: #52-owin-d-support-dictionary-(client)
   [17]: #53-owin-d-capabilities-api-refereince
   [18]: #6-error-handling
   [19]: #61-application-errors
   [20]: #62-server-errors
   [21]: #7-versioning
   [22]: #8-extensions
   [23]: #9-real-world-usage
   [24]: http://www.ietf.org/rfc/rfc2119.txt
   

