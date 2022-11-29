---
description: 168 assignment type beat
---

# The Design Philosophy of the DARPA Internet Protocol

{% embed url="https://web.stanford.edu/class/cs244/papers/DesignPhilosophyDARPA.pdf" %}

## Summary

### Abstract

* The motivation for TCP/IP hadn't been clearly defined, the paper helps clear things up

### Intro

* design has changes
  * ex. connectionless service, layering TCP/IP in different layers
* Paper catalogs one view of the original objectives of the Internet architecture

### Fundamental Goal

* To effectively use existing networks in a multiplexed way
* Components of Internet were networks, which were to be interconnected
* Another idea was to recreate a unified network, but it was felt it would be better to start with existing network architectures
* Packet switching was selected as the multiplexing method
  * existing networks already used packet switching
* We must also use a layer of routers to interconnect the networks

### Second Level Goals

* The previous section doesn't clearly define "effective", here are more detailed goals in order of importance:
  * Internet must continue despite loss of routers
  * Internet must support multiple types of communications service
  * Internet must accommodate a variety of networks
  * Internet must permit distributed management of rescources
  * Internet must be cost effective
  * Internet must permit host attachment with low level effort
  * Resources using in the internet must be accountable
* Context: designed around wartime, so survivability outweighed accountability for example
* The list is more so a list of priorities rather than a "motherhood" list

### Survivability in the Face of Failure

* The most important goal was for the Internet to work despite networks/routers failing
* Connectivity should only be lost if there is absolutely not physical path between hosts
* State information must be protected
  * includes num packets transmitted, ACKed, and outstanding&#x20;
  * Lower layers can't tell if data is lost, so it was insisted info couldn't be lost here
* Fate-sharing is the model that suggests it is fine to lose state info if the entity itself is lost
  * Info above transport layer is stored at hosts
  * Consequence One: routers can't have essential state info, they are stateless
  * Consequence Two: more trust is placed in the hosts, they must ensure connectivity

### Types of Service

* The second goal is to support, at transport layer, a variety of service types
* Diff types have diff speed, latency and reliability constraints
* TCP was made with "virtual circuits" services in mind, such as file transfer
  * even this service had variants based on task specific constraints
  * originally meant to work for all, but soon became clear it couldn't generalize to all
* The realization that multiple transport protocols were needed lead to the separation of IP and TCP, which were originally implemented together as one layer

### Varieties of Networks

* It was important for the Internet to be able to support a variety of network technologies
* It achieves this by making a minimum set of assumptions about the function which the net will provide, including:
  * The network can transmit a packet
  * The packet will be a reasonable size and will be delivered with reasonable reliability
  * Network can address if it is more than a point to point link
* Other services are not explicitly assumed, such as sequences delivery or priority ranking
* Supporting these extra things in the network was not felt to be great as it required a lot of work
* Engineering these things at transport layer only has to be done once at each host
