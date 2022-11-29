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

### Other Goals

* The other goals were lower priority and thus not as fully met
* Distributed management of resource has been done well
  * there are several different router managers
  * there is a routing algorithm that permits routers from diff managers to exchange tables
  * managers of routers are not always the same as the manages of the networks that use them
* There are still issues however with distribution, specifically the tools
  * routing decisions are constrained by policies, which often involve manual setting of tables
* Internet is not always cost effective, packet heads can be very large compared to actual data
* Retransmission is also inefficient as the network doesn't keep track of lost packets
  * The tradeoffs above made acceptable, especially if loss rates are low
* Originally implementing protocols at the host was tough for programmers&#x20;
* Poor implementation of protocols at the hosts may decrease network performance
* Accountability was in the early states of research at the time of this paper

### Architecture and Implementation

* The Internet was designed very heavily around supporting a variety of services and networks
* The ability of the internet to support many varieties of realizations leads to much more engineering to be done when actually designing a new realization
  * It was a struggle to give guidance to engineers working on new realizations
  * Protocol verifiers ensure specs are met, but never deal with performance issues
  * These verifiers were much more concerned with verifying logical correctness
* There was a lack of effective simulators at the time of this paper
  * engineers were more concerned with the service working that the last squeezing out the maximum efficiency or line utilization
* The designers felt it was a mistake to only consider logical correctness, but failed to formalize any aspect of performance constraints within the architecture

### Datagrams (Packets)

* Packets eliminate the need for connection state within routers
* Packets provide a building block for a variety of service types
* Packets represent the minimum network service assumption

### TCP

* TCP designers thought flow control based on bytes and packets was overly complex
* They decided to regulate the flow of bytes based on byte number rather than packets
  * They could insert control info into the sequence space of bytes, though this original idea has been dropped due to the complexity in practice
  * It permits TCP packets to be broken into smaller segments if needed
    * This function was later moved to the IP layer
  * Permits a number of small packets to be gathered into a larger packet
    * this lead to retransmission being must more effectively than sending many small ones
  * Packet based has a severe limit on the throughput of small packets

