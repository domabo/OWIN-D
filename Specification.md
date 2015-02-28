[![OWIN-D](./owin-d.png)](http://owind.org)
#Specification v0.9 RELEASE
* Author : OWIN-JS working group
* Copyright : OWIN-JS contributors
* License : [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/us/)

## Contents

1\. [Overview][1]

2\. [Definitions][2]

3\. [Request Execution][3]

3.1. [Application Delegate][4]

3.2. [Environment][5]

3.3. [Headers][6]

3.4. [Request Body][7]

3.5. [Response Body][8]

3.6. [Request Lifetime][9]

4\. [Application Startup][10]

5\. [URI Reconstruction][11]

5.1. [URI Scheme][12]

5.2. [Hostname][13]

5.3. [Paths][14]

5.4. [URI Reconstruction Algorithm][15]

5.5. [Percent-encoding][16]

6\. [Error Handling][17]

6.1. [Application Errors][18]

6.2. [Server Errors][19]

7\. [Versioning][20]

8\. [Extensions](#8-extensions)

## 1\. Overview

The purpose of this OWIN-D specification is to provide an abstraction from any IoT (Internet of Things) or Web Services for Devices protocol.

OWIN-D defines a standard framework for REST device containers written for io.js, Node.js and application/device logic. It works with any protocol such as COAP, WSDP, OIC iotivity, Apple HomeKit, and can be a drop-in replacement for existing frameworks such as Connect/Express to re-use existing code.

OWIN-D is an extension of the OWIN-JS specification specifically targeted for Internet of Things manufacturers and application developers.

The goal of OWIN-D is to decouple transport and device logic and, by being an open standard, stimulate the open source ecosystem of Node.js web application/device development tools, without ties to any one framework or device protocol.

OWIN-D expands the REST philosophy to web servers, internet of things, etc.

OWIN-D is defined in terms of a delegate structure. There is no assembly. Implementing either the host or application side the OWIN-JS spec does not introduce a dependency to a project.

In this document, the Node.js `function` and C# `Action`/`Func` syntax is used to notate some delegate structures.   However, the delegate structure could be equivalently represented with other native functions, CLR interfaces, or named delegates. This is by design; when implementing OWIN-D, choose a delegate representation that works for you and your stack.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119][21].


## OWIN-D Functions

### Register and Advertise Device/Service/Resource

### Invoke handler for requested resource operation  (server)

### Publish Event to all Subscribers (server)

### Request Resource Operation  (client)

### Stop Advertising

### Discovery Probe
 
Find the devices that meet the given criteria (all, of type lighting, etc.)

### Discovery Resolve

Find the current URIs for a given device URN


## OWIN-D Properties

### Device Info

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Manufacturer** | Name of the manufacturer of the DEVICE. It MUST have fewer than 256 Unicode characters
Yes | **owind.ManufacturerUrl** | URL to a Web site for the manufacturer of the DEVICE. It MUST have fewer than 2,048 octets.
Yes | **owind.ModelName** | User-friendly name for this model of device chosen by the manufacturer. It MUST have fewer than 256 Unicode characters
Yes | **owind.ModelNumber** | Model number for this model of DEVICE. It MUST have fewer than 256 Unicode characters.
Yes | **owind.ModelUrl** | URL to a Web site for this model of DEVICE. It MUST have fewer than 2,048 octets.
Yes | **owind.PresentationUrl** | URL to a presentation resource for this DEVICE. It MAY be relative to the transport address over which metadata was retrieved, and MUST have fewer than 2,048 octets.  If PresentationUrl is specified, the DEVICE MAY provide the resource in multiple formats, but MUST at least provide an HTML page.  CLIENTs and DEVICEs MAY use transport content negotiation [e.g., HTTP/1.1, COAP/1.0] to determine the format and content of the presentation resource.  DEVICEs that use a relative URL MAY use Transport Redirection (e.g., 3xx codes for HTTP/1.1) to direct CLIENTs to a dedicated content server running on another port.


``` js
context["owind.Manufacturer"] = "Domabo";
context["owind.ManufacturerUrl"] = "http://domabo.com";
context["owind.ModelName"] = "Domabot X500";
context["owind.ModelNumber"] = "D-X500";
context["owind.ModelUrl:"] = "http://domabo.com/products/domabot/x500";
context["owind.PresentationUrl"] = "/img/img.jpg";
``` js


### Device Info

#### Model Definitions

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Manufacturer** | Name of the manufacturer of the DEVICE. It MUST have fewer than 256 Unicode characters
No | **owind.ManufacturerUrl** | URL to a Web site for the manufacturer of the DEVICE. It MUST have fewer than 2,048 octets.
No | **owind.ModelName** | User-friendly name for this model of device chosen by the manufacturer. It MUST have fewer than 256 Unicode characters
No | **owind.ModelNumber** | Model number for this model of DEVICE. It MUST have fewer than 256 Unicode characters.
No | **owind.ModelUrl** | URL to a Web site for this model of DEVICE. It MUST have fewer than 2,048 octets.
No | **owind.PresentationUrl** | URL to a presentation resource for this DEVICE. It MAY be relative to the transport address over which metadata was retrieved, and MUST have fewer than 2,048 octets.  If PresentationUrl is specified, the DEVICE MAY provide the resource in multiple formats, but MUST at least provide an HTML page.  CLIENTs and DEVICEs MAY use transport content negotiation [e.g., HTTP/1.1, COAP/1.0] to determine the format and content of the presentation resource.  DEVICEs that use a relative URL MAY use Transport Redirection (e.g., 3xx codes for HTTP/1.1) to direct CLIENTs to a dedicated content server running on another port.


#### Device Definitions

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Id** | Persistent identifier for this DEVICE, typically the MAC address;  the DeviceId MAY be stable for as long as a DEVICE is in a given HOME/network
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
context["owind.ModelUrl:"] = "http://domabo.com/products/domabot/x500";
context["owind.PresentationUrl"] = "/img/img.jpg";
context["owind.DeviceId"] = "1A:2B:3C:4D:5E:FF";
context["owind.DeviceUrn"] = "urn:af6aacb6-17e0-45aa-9fc0-c4090f9c1f53";
context["owind.SetupCode"] = "098-45-211";
context["owind.FriendlyName"] = "LimeRun Test OWIN-D Server";
context["owind.SerialNumber"] = "1234567890";
context["owind.FirmwareVersion"] = "0.85A";
``` 

#### Service Definitions

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Urn** | Unique Resource Name of the service
Yes | **owind.ResourcePath** | The OWIN-JS request path. The path MUST be relative to the "root" of the application CONTAINER, and for a SERVICE or DEVICE MUST be the base onto which [well-known](http://tools.ietf.org/html/rfc5785) sub-paths (e.g., "/oc/core" or ".well-known/core") are appended;  not necesssarily persistent across reboots of the CONTAINER but SHOULD NOT change due to arbitary network reconfigurations
Yes | **owind.ServiceType** | The OWIN-D service type or custom type URN
Yes | **owind.FriendlyName** | User-friendly name for this SERVICE. It MUST have fewer than 256 Unicode characters
No | **owind.Resources** | Array of RESOURCE property dictionaries
No | **owind.Parent** | Reference to parent DEVICE properties dictionary

### Resource Definitions

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Urn** | Unique Resource Name of the service
Yes | **owind.ResourcePath** | The OWIN-JS request path. The path MUST be relative to the "root" of the application CONTAINER, and for a SERVICE or DEVICE MUST be the base onto which [well-known](http://tools.ietf.org/html/rfc5785) sub-paths (e.g., "/oc/core" or ".well-known/core") are appended;  not necesssarily persistent across reboots of the CONTAINER but SHOULD NOT change due to arbitary network reconfigurations
Yes | **owind.ResourceType** | The OWIN-D resource type or custom type URN
Yes | **owind.FriendlyName** | The user-friendly name for this RESOURCE. It MUST have fewer than 256 Unicode characters
Yes | **owind.ResourceInterface** | The OWIN-D interface type (e.g., binary switch)
No | **owind.Parent** | Reference to parent SERVICE properties dictionary

### Optional Resource Format Definitions
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
serviceProperties["owind.ResourcePath"] = [ "/device1/lightservice" ]
brightnessProperties["owind.RequestPath"] = [ "http://127.0.0.1:12001/device1/lightservice/brightness" ];
``` 

## OWIN-D Containers

A container is just a special form of an OWIN Device

that MAY contain

 Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
No | **owind.Devices** | Array of DEVICE property dictionaries


## OWIN-D Server Capabilities

The application startup properties dictionary and each request will contain ["server.Capabilities"] object containing:

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.Version** | "1.0"
Yes | **owind.Support** | OWIN-D Support Dictionary below 

### OWIN-D Support Dictionary

Required | OWIN-D Key Name | Value Description
:------: | ------------- | -------------------------------------
Yes | **owind.RegisterDevice** | {promise} function({dictionary} deviceContext) to register and start advertising the included device definition(s)
Yes | **owind.UnregisterDevice** | {promise} function({string} Urn) to stop advertising the referenced device Urn
Yes | **owind.RegisterResourcePublisher** | {{promise} function(outgoingContext)} function({string} url) to publish OWIN Response Context to all subscribers for this 


### Register and Advertise Device/Service/Resource

### Invoke handler for requested resource operation  (server)

### Publish Event to all Subscribers (server)

### Request Resource Operation  (client)

### Stop Advertising

### Discovery Probe
 
Find the devices that meet the given criteria (all, of type lighting, etc.)

### Discovery Resolve

Find the current URIs for a given device URN






   [1]: #Overview
   [2]: #2-definitions
   [3]: #3-request-execution
   [4]: #31-application-delegate
   [5]: #32-environment
   [6]: #33-headers
   [7]: #34-request-body-100-continue-and-completed-semantics
   [8]: #35-response-body
   [9]: #36-request-lifetime
   [10]: #4-application-startup
   [11]: #5-uri-reconstruction
   [12]: #51-uri-scheme
   [13]: #52-hostname
   [14]: #53-paths
   [15]: #54-uri-reconstruction-algorithm
   [16]: #55-percent-encoding
   [17]: #6-error-handling
   [18]: #61-application-errors
   [19]: #62-server-errors
   [20]: #7-versioning
   [21]: http://www.ietf.org/rfc/rfc2119.txt

