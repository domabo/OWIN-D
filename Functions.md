[![OWIN-D](./owin-d.png)](http://owind.org)
# Core Functions

## Definitions

THe OWIN-D specification provides for a number of common functions that apply to nearly all IoT (Internet of Things) or device networks, regardless of transport protocol (IP, bluetooth, radio wave, etc.)

* **Discovery** &mdash; A set of coordinated peer and/or registry functions that allow ecosystem things to find and connect to each other.  

* **Transfer** &mdash; An operation that is sent to a RESOURCE on a target DEVICE within the ecosystem. Examples include "GET", "SET" or "PLAY".  It MAY return a response.

* **Eventing** &mdash; The ability for a subscriber to receive a periodic stream of observations from a publisher

These core functions MAY abstract and include underlying functions such as **meta data exchange**, **pairing**, **acknowledgments**, **confirmable send**, **policy**, **security**, etc.   Equally these functions SHOULD be available as explicit extensions in the environment dictionary.


## Discovery 

### Register

Function that registers a DEVICE or SERVICE and starts advertising it on the underlying transport server.  Advertising includes sending HELLO messages, and responding to discovery probe and resolve messages.

### Unregister

Function that stops advertising a registered device.

### Probe

Function that probes for a DEVICE in the local ECOSYSTEM.  

### Resolve

Function that resolves the transport location for a given DEVICE by unique identifier in the local ECOSYSTEM.  

## Transfer 

### CreateTransferRequest

Function that creates an an outgoing request to a given resource.   

## Eventing 

### Register

Function that registers a RESOURCE and makes it available to register subscribe requests.

### Unregister

Function that stops publishing events for a registered RESOURCE.

### SendObservation

Function that sends an event observation to all current subscribers for the resource

### CreateTransferRequest

See Transfer section above.  Optionally subscribes to all future observations for this remote resource
