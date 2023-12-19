---
title: "Use cases with Requirements for Packet Optical Integration (POI) Under ACTN Framework"
abbrev: "POI Requirements"
docname: draft-poidt-ccamp-actn-poi-pluggable-usecases-latest

stand_alone: true
ipr: trust200902
area: Routing Area
wg: ccamp
cat: info
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"

keyword:
 - coherent
 - photonic
 - pluggable
 - plugs
 - CMIS
 - I2C
 - OpenConfig
 - Optical
 - Packet

author:
  -
    ins: O. G. de. Dios
    fullname: Oscar Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com

  -
    ins:  E. J. Echeverry
    name: Edward James Echeverry
    org: Telefonica
    email: edward.echeverry@telefonica.com

  -
    ins: R. Rokui
    name: Reza Rokui
    org: Ciena
    email: rrokui@ciena.com
  
  -
    ins: N. Davis
    name: Nigel Davis
    org: Ciena
    email: ndavis@ciena.com    

  -
    ins: B. Vadhadiya
    fullname: Bhavit Vadhadiya
    organization: Vi
    email: bhavit.vadhadiya1@vodafoneidea.com
  
  -
    ins: P. Maheshwari
    fullname: Praveen Maheshwari
    organization: Airtel
    email: Praveen.Maheshwari@airtel.com

  -
    ins: I. Busi
    fullname:  Italo Busi
    organization: Huawei Technologies
    email: italo.busi@huawei.com
  
  -
    ins: A. Guo
    fullname: Aihua Guo
    organization: Futurewei Technologies
    email: aihuaguo.ietf@gmail.com     

contributor:

normative:

   OIF-CMIS:
              title: "OIF Implementation Agreement (IA) Common Management Interface Specification (CMIS))"
              date: 2022-04-27  
              target: https://www.oiforum.com/wp-content/uploads/OIF-CMIS-05.2.pdf

informative:
   pluggables-operators-requirements:
              title: "Operator’s Requirements to support Router Optical pluggable interfaces"
              date: 2023-11-23
              target: https://datatracker.ietf.org/meeting/118/materials/slides-118-ccamp-07-applicability-of-actn-to-poi-extensions-to-support-router-optical-interfaces

   actn-rfc:
              title: "Framework for Abstraction and Control of TE Networks ACTN"
              date: 2018-12-19
              target: https://datatracker.ietf.org/doc/rfc8453/

   draft-davis-ccamp-photonic-plug-control-arch-02:
              title: "Control Architecture of Optical Pluggables in Packet Devices Under ACTN POI Framework"
              date: 2024-01-01
              target: https://datatracker.ietf.org/doc/draft-davis-ccamp-photonic-plug-control-arch/02/

   MANTRA-whitepaper-IPoWDM-convergent-SDN-architecture:
              title: "IPoWDM convergent SDN architecture - Motivation, technical definition & challenges"
              date: 2022-08-31 
              target: https://telecominfraproject.com/wp-content/uploads/TIP_OOPT_MANTRA_IP_over_DWDM_Whitepaper-Final-Version3.pdf          

   ITU-T G.sup39:
              title: "ITU-T Recommendation G.Sup39 (02/16): Optical system design and engineering considerations"
              date: 2016-02-26
              target: https://www.itu.int/rec/T-REC-G.Sup39-201602-I/en  

--- abstract

This document provides general overarching guidelines for control and management of packet over optical converged networks and focuses on operators' use cases with requirements and network topologies. It provides a set of use cases and requirements which are needed to achieve full automation for control and management of the packet over optical networks which comprise devices with mixes of packet and optical functions where the optical functions may be provided on coherent pluggables. 

It is intended that other IETF drafts in this area reference this draft and abide by the use cases and requirements in this draft.

The realization of these use cases is out of scope of this draft and shall be covered in other IETF drafts. 

--- middle

# Terminology
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT"
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in the
document are to be interpreted as described in {{!RFC2119}}.

The following terms abbreviations are used in this document:

* Coherent plug/pluggable: A small form factor coherent optical module
* O-PNC: The control functions specializing in management/control of optical and photonic functions (virtual or physical). See {{actn-rfc}}
* P-PNC: The control functions specializing in management/control of packet functions (virtual or physical). See {{actn-rfc}}
* xPonder: Short for Transponder and/or Muxponder

# Introduction

Packet traffic has been transferred over optical networks for many years blending the benefits of optical transmission and switching with packet switching. Optical systems have been separated from packet systems, both of which have had specific dedicated devices. In many existing network deployments, the packet and the optical networks are engineered, operated and controlled independently. The operation of these packet and optical networks is often siloed which results in non-optimal and inefficient networking. Both packet and optical systems have had relatively independent evolution. Optical systems have been developed with increasing capacity especially with the emergence of coherent optical techniques.

Optical component design has continued to improve density to the point where a whole coherent optical terminal system that use to require many circuit packs can now fit onto a single small form factor "coherent plug". Placing coherent plugs in a device with packet functions can reduce network cost, power consumption and footprint as well as improve data transfer rates, reduce latency and expand capacity (note that in some cases, other engineering and deployment considerations still lead to separate packet and optical solutions). 

Optical transmission/switching is analogue and requires complex and holistic control. Consequently, coordination of control of the coherent plugs (in a device with packet functions) with the control of the rest of the optical network is highly desirable as this best enables robust network functionality and simplifies network operations.

The combination of these above trends along with the desire to select best in breed components has led to the emergence of open optical plugs that offer a standard bus for traffic and that use CMIS {{OIF-CMIS}} between coherent pluggables and host device. These plugs are such that a plug from vendor X can be installed in vendor Y's device with packet functions etc.

An architecture analysis has been carried out by the MANTRA sub-group in the OOPT / TIP group (Open Optical & Packet Transport / Telecom Infra Project) {{MANTRA-whitepaper-IPoWDM-convergent-SDN-architecture}}. 

This document provides guidellines for control and management of packet over optical converged networks and it is divided into following sections:

* Section 3 Packet over optical converged network context
* Section 4 Converged packet over optical networks
* Section 5 Network Topologies
* Section 6 Operators' Use cases with Requirements for Automation of Packet over Optical Converged Networks

# Packet over Optical Converged Network Context

A packet over optical network represents an efficient paradigm that harnesses the power of both packet-switching and optical technologies. In this approach, the overlay IP or MPLS packets are transmitted through an underlying optical network. The fusion of packet and optical networks offer a host of advantages, including accelerated data transfer rates, diminished latency, and expanded network capacity. 

In general, two deployment models can be used to deploy the packet over optical networks: 

* Traditional architecture deployment model
* Deployment model with coherent pluggables

## Traditional Architecture Deployment Model

The traditional architecture involves separation of the packet network from the optical network as shown in {{figure-traditional}}. In traditional approach, the packet layer responsible for routing and forwarding is decoupled from the underlying optical transport layer. This approach offers several benefits, including the ability to scale each layer independently, optimize resource utilization, and simplify network management through centralized software control. 

Disaggregation enables network operators to choose best-of-breed components for each layer, fostering innovation and competition in the networking industry. However, implementing and managing a disaggregated network also comes with challenges related to interoperability, integration, and maintaining end-to-end performance across the various layers.

~~~
      |----------|                                   |----------|
      |  Packet  |           IP Link                 |  Packet  |
      |  Device  |===================================|  Device  |
      |    1     |\                                 /|     2    |
      |----------| \   Grey                        / |----------| 
                    \  Optics                     /
                     |                           |        
        ............ | ......................... | ............
        .            |                           |            .
        .    |---------|     |-----------|     |---------|    .
        .    | xPonder |-----| Photonics |-----| xPonder |    .
        .    |---------|     |-----------|     |---------|    . 
        .......................................................

        Optical Network = Photonics + xPonder

  Legend:
    ====       IP Link
    ----       Optical fibers
    ++++       Coherent pluggables
    xPonder:   Muxponder or transponder 
    Photonics: ROADM + Amp + Regen
~~~
{: #figure-traditional title="Packet over Optics Traditional Architecture Deployment Model"}

## Deployment Model with Coherent Pluggables

The second approach is to take advantage of the small implementation footprint of the xPonder functions and to deploy these functions on a single small form factor plug (aka Coherent pluggables) and then place plugs directly into the packet devices as shown in {{figure-with-plug}}(A). Placing this small form factor pluggable in a device with packet functions can reduce network cost, power consumption and footprint (when these benefits are not outweighed by other engineering considerations). Depending on the application, distance between packet devices, quality of fibers and so on it might be that there is no need for a ROADM network, i.e., direct connectivity between packet devices via plugs is possible.

By incorporating coherent plugs into routers, network operators can achieve higher data rates, greater spectral efficiency, and improved tolerance to optical impairments. This is especially valuable in scenarios where traditional electronic signaling might encounter limitations. Coherent plugs enable routers to leverage advanced modulation schemes, digital signal processing, and error correction techniques, enhancing their ability to handle complex optical signals.

One of the key advantages of using coherent plugs in routers is the potential to bridge the gap between long-haul and metro networks, providing a seamless and efficient transition of data across various network segments. This technology can contribute to the evolution of high-speed data centers, interconnection between data centers, and the overall growth of data-intensive applications.

as noted above, for some use-cases when the distance between packet devices is short and optical power of pluggables are enough, the photonics devices might not be needed as shown in {{figure-with-plug}}(B). 

~~~
      |-----------|                               |-----------|
      |  Packet   |           IP Link             |   Packet  |
      |  Device  +++++ ======================= +++++  Device  |
      |    1      |\                             /|     2     |
      |-----------| \                           / |-----------|  
                     \  DWDM Optics            /   
                      |                       |                            
                      |     |-----------|     |      
                      |-----| Photonics |-----|          
                            |-----------|                
          
                                 (A)

      |-----------|                               |-----------|
      |  Packet   |           IP Link             |   Packet  |
      |  Device  +++++ ======================= +++++  Device  |
      |    1      |\                             /|     2     |
      |-----------| \                           / |-----------|  
                     |                         |                            
                     |-------------------------|        

                                (B)

  Legend:
    ====       IP Link
    ----       Optical fibers
    ++++       Coherent pluggables
    xPonder:   Muxponder or transponder 
    Photonics: ROADM + Amp + Regen
    Optical Network: Photonics + pluggables
~~~
{: #figure-with-plug title="Packet over Optics Deployment Model with Coherent Plugs"}

In reality, the operators' packet over optical networks will most likely be a combination of networks shown in {{figure-traditional}} and {{figure-with-plug}} where the optical network contains both coherent pluggables and xPonders as shown in {{figure-with-plug-and-xponder}}.

~~~
      |-----------|                                   |-----------|
      |  Packet   |              IP Link              |   Packet  |
      |  Device  +++++ =========================== +++++  Device  |
      |    1      |\                                 /|     2     |
      |-----------| \                               / |-----------|
                     \----------|     |------------/
                                |     |
             |---------|     |-----------|      |---------|
             |         |     |           |      |         |
             | xPonder |-----| Photonics |------| xPonder |
             |         |     |           |      |         |             
             |---------|     |-----------|      |---------|
                    |                              |
                    |                              |                    
      |----------| /                                \ |----------|
      |  Packet  |/             IP Link              \|  Packet  |
      |  Device  |====================================|  Device  |
      |    3     |                                    |     4    |
      |----------|                                    |----------|

      Optical Network: Photonics + pluggables + xPonder

  Legend:
    ====       IP Link
    ----       Optical fibers
    ++++       Coherent pluggables
    xPonder:   Muxponder or transponder 
    Photonics: ROADM + Amp + Regen
~~~
{: #figure-with-plug-and-xponder title="Packet over Optics Deployment Model with Coherent Plugs and xPonders"}

# Converged Packet Over Optical Networks

This section provides an overview of converged packet-optical networks from various perspectives.

## Logical view of control of converged packet optical networks

{{figure-traditional}} and {{figure-with-plug}} represent two deployment models which can be used to deploy the packet over optical networks. In reality the operators' networks are mix of both deployments, i.e., operators will have a packet over optical network which contains packet devices, coherent pluggables, muxponders/transponders and photonics such as ROADMs.

The high level control and management of such packet over optical converged network is shown in {{figure-poi-control}} where the "PACKET OPTICAL NETWORK" contains any combination of devices with any mix of packet functions and optical functions. These networks might include coherent pluggables, muxponders/transponders and ROADMs. 

As shown in {{figure-poi-control}}, the "PACKET AND OPTICAL CONTROLLERS" layer may contain one or more packet and optical control functions which manage and control the life cycle of end to end packet and optical services including planning, fulfilment, assurance, optimization and restoration. 

Depends on operators' use-cases which should be supported by packet over optical converged network, there might be a " HIGHER LAYER CONTROLLER" (i.e., higher layer multi-layer Orchestrator or multi-layer proxy).

Realization of this functional architecture is proposed by various SDOs. For example, an architecture analysis has already been carried out by the MANTRA sub-group in the OOPT / TIP group (Open Optical & Packet Transport / Telecom Infra Project) {{MANTRA-whitepaper-IPoWDM-convergent-SDN-architecture}}. 

Section 5 covers the requirements of these controllers to achieve full automation in packet over optical converged networks.

~~~ 
             |-----------------------------|
             |   HIGHER LAYER CONTROLLER   |
             |            (MDSC)           |
             |-----------------------------|
                            ^    
                            | 
                            v          
         |-------------------------------------|
         |            P-PNC & O-PNC            |
         |                                     |
         | |-------------|     |-------------| |
         | | Packet      |  &  | Optical     | |
         | | Control     |     | Control     | |
         | | Functions   |     | Functions   | | 
         | |-------------|     |-------------| |
         |-------------------------------------|
                            ^   
                            |  
                            v  
           /----------------------------------\
          /      PACKET OPTICAL NETWORK        \
         /                                      \ 
         \     Packet and Optical Functions     /
          \    in various devices              /
           \----------------------------------/
~~~
{: #figure-poi-control title="Overall Control and Management of Packet over Optical Converged Networks"}

## Logical view of a converged device

All devices are essentially multi-technology, i.e., they support multiple transport and signaling technologies. However, due to implementation limitations and network deployment traditions, there has been a strong division between devices that have sophisticated optical functionality (with very limited packet capabilities) and devices with sophisticated packet functionality (with very limited optical capability). This division is dematerializing with the emergence of devices that support both sophisticated packet and sophisticated optical functionality (were both packet and optical can be considered in themselves a multi-technology).

To enable necessary flexibility of deployment, the optical capabilities are often made available on a coherent plug that can be inserted into a host device. In this document the host device is one with primarily packet functions. A coherent plug can also be used in a device with primarily optical functions, with primarily storage functions, with primarily wireless functions etc., where similar considerations apply. 

The coherent plug includes both the optical functions that provide the transport and their control functions. It is necessary to access the control data related to the coherent plug via interfaces on the host devices. The combination of the host device and the coherent plug can be considered as a packet-optical device. 

The functions provided by the coherent plug include the line termination functions of a traditional optical transponder. The insertion of these functions into the host device removes the need for grey optics between the host device and a transponder.

As depicted in {{figure-details-packet-optical-device}}, in the packet-optical device there is a clear demarcation between the functions and data that relate to packet control and the functions and data that relate to optical control where the boundary between packet functionality and optical functionality is at the boundary between the plug and the host device. 

~~~          
                     ^ 
                     | 
                     v
  +-----------------------------------+        
  |  |-----------|      |----------|  |      
  |  | Packet    |      | Coherent |  |   
  |  | Function  |      | Plug     |  | 
  |  | Control   |      | Control  |  |   
  |  | Data      |      | Data     |  |   
  |  |-----------|      |----------|  | 
  |        .                   .      |                
  |  |-------------|           .      |                ^
  |  |Packet       |           .      |                |
  |  |Control      |           .      |                v
  |  |-------------|           .      |        +----------------+ 
  |        .                   .      |        |                |
  |  |-------------|         |----------|      |                | 
  |  |Packet       |<------->| Coherent |======|     ROADM      |
  |  |Function     |         | Plug     |      |                | 
  |  |-------------|         |----------|      |                |
  |                                  |         |                |
  +----------------------------------+         +----------------+

         PACKET DEVICE with Plugs                OPTICAL DEVICE  

~~~
{: #figure-details-packet-optical-device title="Packet device which contains coherent pluggables"}


## End-to-end optical network

It is best to consider any network technology/protocol/application from end to end. Each network technology provides infrastructure for an overlay technology which may be another network technology or to an actual application (storage, compute, etc.), i.e., it provides a "link" with capacity etc. Considering the converged packet-optical solution, the optical technologies provide infrastructure to the packet technologies.

The optical network includes all functions that process optical technologies and hence include functions on devices such as a ROADM, an optical amplifier, a transponder and the functions on the coherent plug. The boundary of the optical technologies is at the boundary between the coherent plug and the host device.

Optical networks complexity depends upon transmission distance, need for flexibility in the photonic layer and need for photonic resilience.

## Complexity of optical network operation

The operation of a network of coherent optical devices can be very complex requiring careful consideration of various analogue properties of the optical devices, of passive components and of the current usage of the optical network. This complexity leads to the need for a set of specialist optical control functions that have traditionally been provided as part of an Optical Domain Controller (similar to the need for specialist IP control functions).

## Converged packet optical network operation

In a converged network it is necessary to combine the specialist control functions for the packet network functions and specialist control functions for optical network functions. There are various potential solutions for this combining. In this document, it is assumed that a higher layer controller will provide the solution focusing on converged visualization, optimization, assurance etc. 

It is important to recognize that in any real network deployment there will be a mix of converged solutions and traditional solutions where there will probably be a gradual evolution away from traditional forms to converged forms. It will be necessary for any control solution to deal with the mix and its evolution.

In all cases, it is necessary to evaluate options to determine the best optical network solution (see {{ITU-T G.sup39}} for engineering considerations). Hence, in a network where there are various solutions, even for situations where a basic direct grey interconnect turns out to be the right configuration, it is necessary to analyze the network in detail to determine this. Hence, it is necessary to involve the optical control functions in all decisions about optical network configuration. 

For some restoration cases there is a need for near real time optical configuration. The pluggable settings may need to be adjusted during restoration control actions. For example, it is possible that regeneration may be identified as required during a restoration activity and that as a result of this or other considerations, optical parameter changes, including wavelength and power may need to be applied to a pluggable during normal operation.

## Commissioning of coherent plugs

Commissioning of more capable, and hence expensive, coherent plugs in routers tends to follow a just-in-time deployment pattern where the pluggables are not installed in the host device until they are required for service. The pluggables used in more challenging applications require sophisticated photonic viability assessment. The specialist photonic viability tools reside in the optical control function set.

Where there is a need to install a new pluggable, the process will operate in a relatively slow time frame. Once the pluggables are detected by the optical controller the parameters of the pluggables can be configured and progress through any necessary validation testing on the optical network. This testing may involve the need to control the pluggables optical parameters along with parameters of other devices supporting the optical/photonic signals.

## Generalized optical control

Industry is progressing towards generalized optical viability functions but currently, these functions tend to be vendor specific and reside in the vendor controllers. Current deployments tend to have a generalized optical controller from a particular optical device vendor controlling other vendor optical controllers. Where optical control is discussed in this document, it is assumed to be the collection of all optical control capabilities including whatever assembly of vendor controllers and generalized controllers are present.

Note that it is the expectation that a single optical controller will provide the control functionality of all coherent plugs in a specific host device regardless of the mix of plugs from different vendors.

# Network Topologies

This section provides a set of packet over optical network topologies starting with the most basic and progressing to the most complex. It is expect that a network will evolve to a mix of many of the structure identified in each of the following sections. 

All the packet over optical use cases outlined in Section 7 will be applicable to any on these network topologies.

## Topo1 - Network topology with dedicated direct fiber

As depicted in {{figure-topo1}}, this scenario considers a point-to-point optical service over a short distance (e.g., up to 100 km) using dedicated fiber. ({{pluggables-operators-requirements}}, Page 4, "Dedicated point to point connection Metro areas").

Note that there is no amplification and no protection in this scenario.

~~~
    Packet                                                             Packet
    Device A                                                           Device B
    +----+             IP Link (between Router Ports)                  +----+
    |    |.............................................................|    | 
    |    |                                                             |    |
    |    |             Optical Service (Plug-to-Plug)                  |    |    
    |    |    .....................................................    |    |
    |  |------|                                                   |------|  | 
    |  |      |                                                   |      |  |
    |  |Plug A|===================================================|Plug B|  |
    |  |      |                                                   |      |  |
    |  |------|                                                   |------|  |
    |    |                                                             |    | 
    +----+                                                             +----+
~~~
{: #figure-topo1 title="Network topology with dedicated direct fiber"}

## Topo2 - Network topology with shared direct fiber network

This scenario extends {{figure-topo1}} by making more efficient use of the fiber infrastructure. 

As shown in {{figure-topo2}}, this scenario considers a point-to-point optical service over a short distance (e.g., up to 100 km) using a physical optical network with DWDM filters and amplifiers. ({{pluggables-operators-requirements}}, Page 4, "Dedicated point to point connection Metro areas").

Note that there is no protection in this scenario.

~~~   
    Packet                                                             Packet
    Device A                                                           Device B
    +----+             IP Link (between Router Ports)                  +----+
    |    |.............................................................|    |
    |    |                                                             |    |
    |    |             Optical Service (Plug-to-Plug)                  |    |    
    |    |    .....................................................    |    |
    |  |------|                                                   |------|  | 
    |  |      |      |-------|      |-------|      |-------|      |      |  |
    |  |Plug A|======| Filter|======|  AMP  |======| Filter|======|Plug B|  |
    |  |      |  ||==|       |      |       |      |       |==||  |      |  |
    |  |------|  ||  |-------|      |-------|      |-------|  ||  |------|  |
    |    |       ||                                           ||       |    | 
    +----+       ||                                           ||       +----+
                 ||                                           ||
       |------|  ||                                           ||  |------|
       |      |==||                                           ||==|      |
       |Plug C|                                                   |Plug D|
       |      |                                                   |      |
       |------|                                                   |------|
~~~
{: #figure-topo2 title="Network topology with shared direct fiber network"}

## Topo3 - Network topology with shared switched fiber network

This scenario extends {{figure-topo2}} by making more flexible use of the fiber infrastructure. 

As shown in {{figure-topo3}}, this scenario considers a point-to-point optical service over longer distance (e.g., up to 500 km) using a flexible physical optical network with DWDM filters, amplifiers and optical switching. ({{pluggables-operators-requirements}}, Page 4, "Point to point connection over metro/regional areas").

Note that there is no resilience in this scenario.

~~~   
    Packet                                                             Packet
    Device A                                                           Device B
    +----+              IP Link (between Router Ports)                 +----+
    |    |.............................................................|    |
    |    |                                                             |    |
    |    |              Optical Service (Plug-to-Plug)                 |    |    
    |    |    .....................................................    |    |
    |  |------|                                                   |------|  | 
    |  |      |      |-------|      |-------|      |-------|      |      |  |
    |  |Plug A|======| ROADM |======| ROADM |======| ROADM |======|Plug B|  |
    |  |      |      | + Amp |      |       |      | + Amp |      |      |  |
    |  |------|      |-------|      |-------|      |-------|      |------|  |
    |    |                                                             |    | 
    +----+                                                             +----+
~~~
{: #figure-topo3 title="Network topology with shared switched fiber network"}

## Topo4 - Network topology with shared resilient fiber network

This scenario adds optical resiliency to the fiber infrastructure and is applicable to both topologies shown in {{figure-topo2}} and {{figure-topo3}}.  

As shown in {{figure-topo4}}, optical resiliency is achieved by providing alternative path through the optical network. This may be achieved by some combinations of restoration and protection. This scenario is applicable to {{figure-topo2}} and {{figure-topo3}} and restoration additionally is applicable to {{figure-topo3}}.

~~~   

  Packet                                                              Packet
  Device A                                                            Device B
  +----+               IP Link (between Router Ports)                 +----+
  |    |..............................................................|    |
  |    |                                                              |    |
  |    |               Optical Service (Plug-to-Plug)                 |    |    
  |    |    .....................................................     |    |
  |  |------|              |----------------------|              |------|  | 
  |  |      |  |-------| //|      Photonics       |\\ |-------|  |      |  |
  |  |Plug A|==|  OPS  |// |----------------------| \\|  OPS  |==|Plug B|  |
  |  |      |  |       |\\                          //|       |  |      |  |
  |  |------|  |-------| \\|----------------------|// |-------|  |------|  |
  |    |                   |      Photonics       |                   |    | 
  +----+                   |----------------------|                   +----+

 Legend:
   OPS: Optical Protection Switch                         
~~~
{: #figure-topo4 title="Network topology with shared resilient fiber network"}

## Topo5 - Network topology with symmetric plug and xPonder

This scenario shown in {{figure-topo5}} and extends network topologies {{figure-topo1}} to {{figure-topo4}} where one end of an optical service is terminated on a plug and the other end is terminated on a traditional xPonder (transponder or muxponder) potentially with grey optics to a packet device.

~~~
    Packet                                                             Packet
    Device A                                                           Device B
    +----+             IP Link (between Router Ports)                  +----+
    |    |.............................................................|    | 
    |    |                                                             |    |
    |    |     Optical Service (Plug-to-xPonder) |-------|             |    |    
    |    |    ...................................|       |             |    |
    |  |------|                                  |       |             |    | 
    |  |      |    |-----------------------|     |       | Grey Optics |    |
    |  |Plug A|====|        Photonics      |=====|xPonder|=============|    |
    |  |      |    |-----------------------|     |       |             |    |
    |  |------|                                  |-------|             |    |
    |    |                                                             |    | 
    +----+                                                             +----+
                                                            
~~~
{: #figure-topo5 title="Network topology with symmetric plug and transponder"}

## Topo6 - Other Network Topologies

* Network topology with shared switched fiber network with regenerators: This is extension of topology Topo-3 {{figure-topo3}} when the photonic network has regenerator.
* Asymmetric interconnect Network topology where the protection open at one end but both protection legs are terminated on separate xPonder or coherent pluggables.
* IP Lag Network topology where the IP link between two packet devices are provided by multiple coherent plugs
* Practical network deployments which includes the mix of many network topologies explained above.

# Operators' Use cases with Requirements for Automation of Packet over Optical Converged Networks

This section provides a set of packet over optical use cases which are applicable to any network topologies in Section 5. These use cases in turn drives the operators' requirements needed to support the automation of packet over optical converged networks. The use cases and requirements in this section are a combination of functional and operational and are agnostics to their realizations.
See Appendix (A) for details of requirements.

These use cases are grouped into two categories, packet optical infrastructure use cases and multi-layer/end-to-end use-cases:

Packet optical infrastructure use cases:

* UC1 - Infrastructure discovery and visualization of packet optical network: Discovery of optical and packet network topology from L0 optical services to IP links 
* UC2 - Inventory of packet optical network infrastructure: Inventory of optical and packet networks infrastructure
* UC3 - Monitoring of packet optical network infrastructure: Monitoring of the optical and packet networks infrastructure using the telemetry data. This is consider one of the operational use cases.
* UC4 - Optimization of packet optical network infrastructure: Monitor the health of packet and optical infrastructure and perform corrective actions if needed
* UC5 - Optical service provisioning for creation of packet infrastructure: Provisioning of optical and packet network infrastructure from L0 optical services to IP links

Multi-layer/end-to-end use-cases:

* UC6 - Provisioning of an end-to-end packet service: Provisioning of L2/L3 packet services
* UC7 - Multi-layer visualization: From underlay L0 optical services to overlay L3 packet services
* UC8 - Multi-layer assurance and troubleshooting across packet and optical layers
* UC9 - Multi-layer optimization: This is an extension of use case UC5 where the packet services will be considered as well
* UC10 - Multi-layer pro-active maintenance and control coordination
* UC11 - Optical service pre-deployment assessment for IP link creation
* UC12 - Restoration/protection of optical services
* UC13 - Adaptive and dynamic routing Schemes protection for IP services

## UC1: Infrastructure Discovery and Visualization of Packet Optical Network

The use case provides the discovery of packet over optical network which is considered the multi-layer network infrastructure. It includes:

* Discovery of optical physical network (e.g., equipments including optical nodes and coherent plugs)
* Discovery of optical topology (i.e., adjacencies and links)
* Discovery of L0 optical services
* Discovery of packet physical network (e.g., equipments including packet nodes)
* Discovery of packet topology (i.e., adjacencies and IP links)
* Discovery of "interdomain transitional links", i.e., links which connect the optical network to and packet network

Using this information, the solution can discover the multi-layer packet over optical network by correlating the IP links to L0 optical services. Note that the mapping between IP links and optical services might be 1:1, 1:many or many:1. As shown in {{figure-uc1-correlation}}, multi-layer network discovery provides the correlation between various layers from optical services to packet network up to IP link. 

~~~ 
                 <-- IP link between packet devices ---> 
                    <----- L2 Ethernet Service ---->
                       <---- Optical Service ---->
                         <--- Optical Fiber --->

      |-----------|                                  |-----------|
      |  Packet   |            IP Link               |   Packet  |
      |  Device  +++++ ========================== +++++  Device  |
      |    1      |\                                /|     2     |
      |-----------| \  Transitional                / |-----------|  
                     \ Link                       / 
                      |       |-----------|      | 
                      |-------| Photonics |------| 
                              |-----------|   

~~~
{: #figure-uc1-correlation title="Multi-layer Network Discovery"}

Requirements driven by this use case:

* R1: Support for "Coherent Plug Discovery": The solution shall allow the controller to discover the coherent plug state and to configure the coherent plug operation. See [draft-davis-ccamp-photonic-plug-control-arch-02]].
* R2: Support for "Network Discovery": The solution shall provide the multi-layer "Network infrastructure Discovery" ({{pluggables-operators-requirements}}, Page 5 requirement 1).
* R3: Support for "Network Visibility": The solution shall provide the end-to-end multi-layer "Network Visibility and Visualization" ([pluggables-operators-requirements], Page 5 requirement 1).
* R15: Support for operators' operational practices: The solution shall support existing operators' operational practices on packet and optical network and services. See [draft-davis-ccamp-photonic-plug-control-arch-02]. Please note that this requirement is applicable to all use cases.

## UC2: Inventory of packet optical network infrastructure

The discovery process provides inventory for network shown in {{figure-uc1-correlation}}. 

## UC3: Monitoring of packet optical network infrastructure:: 

This use cases covers the real-time collection of "Alarm Event Notification" and "Performance Monitoring (PM)" telemetry data from packet over optical network shown in {{figure-uc1-correlation}}. In other words, by collecting the telemetry data from following network objects, the solution should be able to delete any deterioration to packet optical network infrastructure. 

* Optical physical network (e.g., equipments including optical nodes and coherent plugs)
* optical topology (i.e., adjacencies and links)
* Optical services
* Packet physical network (e.g., equipments including packet nodes)
* Packet topology (i.e., adjacencies and IP links)
* Interdomain transitional links (i.e., links which connect the optical network to and packet network)

Requirements driven by this use case:

* R4: Support for "Coherent Plug telemetry data": See [draft-davis-ccamp-photonic-plug-control-arch-02]
* R5: Support for alarms telemetry across packet and optical layers: his requirement mandates the real-time collection of "Alarm Event Notification" telemetry data from both packet and optical layers ([pluggables-operators-requirements], Page 5 requirements 1 and 6).
* R6: Support for PM telemetry across packet and optical layers: This requirement mandates the real-time collection of performance Monitoring (PM) data from both packet and optical layers ([pluggables-operators-requirements], Page 5 requirements 1 and 6).

## UC4: Optimization of packet optical network infrastructure 

This use case employs the telemetry data collected from packet optical network in use case UC3 to monitor the health of packet and optical infrastructure and performing the corrective actions if needed.

## UC5: Optical service provisioning for creation of packet infrastructure

Referring to {{figure-uc1-correlation}}, this use-case provides the provisioning of new optical services and new packet infrastructure (i.e., IP links). In other words, this use case addresses the provisioning of new optical services from plug-to-plug and mapping them to new IP links.

This use case covers situations when the IP network needs more capacity which in turn means one or more new optical services need to be provisioned. An optical service provides underly infrastructure and hence provides capacity to the IP layer.

This use case involves the following steps:

* Determine the need for new IP capacity
* Identify where that capacity is needed and identify candidate devices to be interconnected
* Assess the optical solution and viability
* Identify the appropriate coherent plugs
* Install and configure the coherent plugs
* Provision one or more optical services between plugs
* Perform test and validation of the optical services (including plugs)
* Make the extra capacity available to the IP network (i.e., to IP links) 

Requirements driven by this use case:

* R7: End-to-end provisioning and deletion of optical services: The solution shall support end-to-end provisioning and deletion of optical services ([pluggables-operators-requirements], Page 5 requirements 2 and 3).


## UC6: Provisioning of an end-to-end packet service

This use-case covers the end-to-end provisioning of a packet VPN service between two ports of packet devices which are equipped with coherent pluggables. 

As depicted in {{figure-uc6-e2e-services}}, before provisioning the packet service between ports A and B on packet devices 1 and 3, two optical services OS1 and OS2 should be created first and mapped to new IP link1 and IP link2, respectively. Then, to facilitate L2/L3 VPN services, an IP/MPLS TE tunnel or alternative technologies such as segment routing, FlexAlgo or SRv6 are deployed. This approach allows for a more versatile and adaptable network configuration to meet different VPN requirements.

~~~ 
          <------------------- VPN Service -------------------->
            <-------------- IP/MPLS TE-Tunnels -------------->
              <--- IP link1 -->            <-- IP link2 --->
               <---- ES1 ---->              <---- ES2 ----> 
                <--- OS1 --->                <--- OS2 --->
                 <-OF-><-OF->                <-OF-><-OF->

    |--------|                 |---------|                 |---------| 
    | Packet |  A              | Packet  |              B  | Packet  | 
    | Device +++ =========== +++ Device  +++ =========== +++ Device  |
    |   1    |\               /|   2     |\               /|   3     |
    |--------| \             / |---------| \             / |---------| 
                \           /               \           /
                 \-----|   |                |   |------/
                       |   |                |   |
                 |---------------------------------------|           
                 |    Photonics (ROADM + Amp + Regen)    |
                 |                  +                    |
                 |                xPonder                | 
                 |---------------------------------------|  

  Legend:
    ES     L2 Ethernet Service
    OS     Optical Service
    OF     Optical Fiber
    ====   IP Link
    ----   Optical fibers
    ++++   Coherent pluggables
~~~
{: #figure-uc6-e2e-services title="End-to-end Packet Services"}


Requirements covered by this use case:

* R7: End-to-end provisioning and deletion of optical services: The solution shall support end-to-end provisioning and deletion of optical services ([pluggables-operators-requirements], Page 5 requirements 2 and 3).
* R8: End-to-end provisioning and deletion of packet services: The solution shall support end-to-end provisioning and deletion of packet services ([pluggables-operators-requirements], Page 5 requirements 2 and 3).

## UC7 - Multi-layer visualization 

Referring to multilayer packet services shown in {{#figure-uc6-e2e-services}}, this use case addresses the visualization multi-layer services from L0 optical services to L2/L3 packet services. Note that this use case employs use cases UC1 and UC2 where the multi-layer packet over optical network is already discovered and inventorized.

## UC8 - Multi-layer assurance and troubleshooting across packet and optical layers

Consider the multi-layer packet over optical network depicted in {{figure-uc6-e2e-services}}. This use case uses UC3 to collect the alarm notifications and PM telemetry data from both packet optical network infrastructure and packet optical services, correlated them together and use this correlation during the passive or pro-active multi-layer troubleshooting and assurance.

Requirements covered by this use case:

* R9: Multi-layer assurance across both packet and optical layers: The solution shall support the multi-layer assurance and troubleshooting across packet and optical layers ([pluggables-operators-requirements], Page 5 requirement 5).

## UC9 - Multi-layer optimization

This use case is an extension of use case UC8 where it employs the telemetry data collected from packet optical network in use case UC8 to monitor the health of multi-layer packet and optical infrastructure and services and to perform any corrective actions if needed.

## UC10 - Multi-layer pro-active maintenance and control coordination

To achieve full automation across optical and packet layers, this use case covers the cross layer control and maintenance operations. Since the optical and packet layers are inter-dependent, any changes to one layer will impact the services in other layer. For example, if an optical link is out of service for maintenance, it will impact one or multiple IP links and packet services. 

This use case provides a pro-active approach (using make-before-break scheme) by informing the other layer before doing any changes. For example, operator can bring an optical link to maintenance. This causes the L0 services using that optical link to be flagged as maintenance which causes all IP links map to L0 services to be flagged as well. This in turn allows the packet layer to drain the appropriate IP links, tunnels and packet services which causes graceful maintenance operations across network.

Considering packet optical network shown in {{figure-uc10-control-coordination}} where operator would like to perform maintenance on optical fiber OF2. Before doing so, operator can put OF2 in maintenance mode. Since "VPN service 1", "TE-tunnel 1", "IP link 1" and "Optical service 1" are all mapped to OF2, operator can put OF2 in "maintenance mode" which causes the packet layer to drain IP link1 and potentially re-router TE-tunnel 1. This pro-active approach causes graceful drainage of packet traffic before maintenance.

~~~   

     <------------------------- VPN service 1 ----------------------->
        <----------------------- TE-tunnel 1 --------------------->

    Packet                                                       Packet
    Device A                                                     Device B
    +----+                                                       +----+
    |    |<--------------------- IP Link 1 --------------------->|    |  
    |    |   <--------------- Optical Service 1 -------------->  |    |
    |    |     <- OF1 ->         <- OF2 ->         <- OF3 ->     |    |  
    |  |------|                                             |------|  | 
    |  |      |         |-------|         |-------|         |      |  |
    |  |Plug A|=========| ROADM |=========| ROADM |=========|Plug B|  |
    |  |      |         |       |    ^    |       |         |      |  |
    |  |------|         |-------|    |    |-------|         |------|  |
    |    |                           |                           |    | 
    +----+            Operator would like to perform             +----+
                      maintenance on this optical fiber


~~~
{: #figure-uc10-control-coordination title="Network topology with shared switched fiber network"}

Requirements covered by this use case:

* R13: Multi-layer control and maintenance operations: The solution shall support the "Multi-layer Control and Maintenance Operations" across packet and optical networks ([pluggables-operators-requirements], Page 5 requirement 8).

## UC11 - Optical service pre-deployment assessment for IP link creation

During creation of a new IP link and before the creation of a new optical service, this use case covers consideration for optical viability, i.e., it considers the processes involved in evaluating optical viability as part of the process of design of the realization of a connection.

Note that the combination of the following two considerations means that it is often not possible to simply turn on an existing physical setup to cause further link capacity to be realized.

Optical transmission is an analogue technology where success is influenced and impacted by real physical conditions and where determining viability is complex. Other than for the most basic short direct optical links, it is necessary to employ optical viability tools to identify necessary intermediate components and define optimum optical set-up.

Optical components are relatively expensive and are often not deployed in the network until needed. As a consequence, there is often no simple potential link opportunity, and instead understanding of optical interconnectability relies on knowledge of semi-abstracted interbuilding fibering, potential plug capabilities and device with packet functions compatibility.

Requirements covered by this use case:

## UC12 - Restoration/protection of optical services

Depend on the operators' requirements for resiliency on packet and optical networks, some operators prefer to have restoration and protection at optical layer. This use case integrates the optical layer protection and restoration including expected configurations, assurance, telemetry collection, optimization and path reversion in a uniform fashion.

If an operator deploys an optical protection scheme, the resiliency can be achieved in sub-ms. However, if they deploy a path restoration scheme, the resiliency will not be in sub-ms range.

Requirements covered by this use case:

* R12: Optical path restoration / protection: Optical path restoration / protection shall be supported ([pluggables-operators-requirements], Page 5 requirement 7).

## UC13 - Adaptive and dynamic routing Schemes protection for IP services

This use case complement UC12 and involves implementing and managing adaptive and dynamic routing protocols to protect IP services against interruptions and provide continuous service. 
It highlights the importance of having flexible routing schemes that are able to respond quickly to changes in the network and thereby maintain optimal network performance and service assurance.

## UC14 - Other Requirements applicable to all use case

There are a set of requirements shown below which are applicable to all use cases. See Appendix (A) for details of these requirements.

* R10: Support operators' realization practices
* R11: LAG extension
* R14: "Single functional entity" responsible for optical services life cycle management
* R16: Support for multi-layer operational benefits
* R17: Support for "greenfield" and "brownfield" networks
* R18: Optional higher level controller
* R19: Support of both plugs and Transponders/Muxponders (inc. Regens)
* R20: Various existing YANG Data Models shall be accommodated
* R21: Clear demarcation for holistic control of optical network
* R22: Support for urgent optical control actions
* R23: Minimize fragmentation of optical parameter provisioning
* R24: Direct path to relevant controller
* R25: Evolution to expected future controller deployment approaches
* R26: Evolution to future packet processing deployment approaches
* R27: Support for extensible control architecture


# Conclusion

This document has provided:

* An overview of converged packet over optical networks from a control perspective focused on the implications of the deployment of coherent plugs in devices with packet functions
* A set of requirements for the operation of a network including coherent plugs
* A progression of use cases covering key areas of operations focusing on coherent plugs
* A set of network topologies which illustrate various coherent plug applications

This document has a broad coverage to encompass all existing and future approaches to deployment and control of photonic plugs.

With the above coverage, this document is suitable to provide an overarching framework for other IETF works on coherent plugs including:

* A functional architecture for control of a multi-technology network (especially a network including coherent plugs:
* Various physical realizations of the functional architecture
* Interaction of a control solution with devices that are equipped with coherent plugs
* Interfaces and models to be used on the devices that are equipped with coherent plugs

It is intended that other IETF drafts in this area reference this draft and abide by the requirements, use cases in this draft.

# Security Considerations


# IANA Considerations

This document has no IANA actions.

--- back

# Details of Operators' Requirements for Automation of Packet over Optical Converged Networks

This appendix outlines the details of operators' requirements needed for any control architecture to support the full automation of packet over optical converged networks.

The requirements in this appendix are driven by a combination of operational and functional considerations and are control solution realization-agnostics.

## R1: Support for "Coherent Plug Discovery"

The host platform (e.g., packet device) shall provide full access to all properties of the coherent plug. This allows the controller to access all config and telemetry information available from coherent plug. As shown in {{figure-plug-data}}, once the coherent plug is inserted into host platform, it shall be recognized by host platform, which shall allow the full access to plug config and telemetry information on interface (A). Once the host platform has full access to plug information, it shall in turn allow this information to be accessed by any controller on interface (B). In other words, both interfaces (A) and (B) shall have access to all plug config and telemetry information.

This will allow the controller to discover the coherent plug state and to configure the coherent plug operation. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}].

All standard data and all proprietary data from the coherent plug should be made available to one or more controllers by the platform hosting the plug. The platform hosting the plug should not attempt to interpret the plug data prior to making it available to a controller. A generic approach to mapping the data to the interface model should be adopted wherever possible. The data should be made available with no intermediate transformation by the platform hosting the plug. All notifications should be propagated transparently (see requirement R4).

It is recognized that some aspects of the plug, such as electrical power consumption, will need to be understood by the host platform control functionality. These properties should be expressed clearly by the plug in a standard, generic and consistent fashion.

~~~          
                        ^ 
                        |
                        v (B)
      +---------------------------------+        
      |  |-----------|    |----------|  |      
      |  | Packet    |    | Coherent |  |   
      |  | Function  |    | Plug     |  |   
      |  | Data      |    | Data     |  |   
      |  |-----------|    |----------|  | 
      |        .                   .    |               
      |        .               (A) .    |       
      |  |-----------|          |----------|   
      |  | Packet    | <------> | Coherent |==== 
      |  | Function  |          | Plug     |
      |  |-----------|          |----------|  
      |                                |           
      +--------------------------------+   

      Host platform (e.g., packet device)      

~~~
{: #figure-plug-data title="Plug discovery by host platform"}

## R2: Support for "Network Discovery" 

The solution shall provide the end-to-end multi-layer "Network Discovery" ({{pluggables-operators-requirements}}, Page 5 requirement 1). It includes:

* Discovery of optical physical network (i.e., optical nodes and fibers)
* Discovery of optical services 
* Discovery of packet network (i.e., IP links and packet devices)
* Discovery of "interdomain transitional links", i.e., links which connect the optical network to and packet network

Using this information, the solution shall discover the multi-layer packet over optical network, i.e., correlation between IP links and optical services. Note that there might be a 1:1, 1:many or many:1 relationship between IP links and optical services. As shown in {{figure-correlation}} multi-layer network discovery provides the correlation between various layers from optical underlay to packet overlay. 

~~~ 
                 <-- IP link between packet devices ---> 
                    <----- L2 Ethernet Service ---->
                       <---- Optical Service ---->
                         <--- Optical Fiber --->

      |-----------|                                  |-----------|
      |  Packet   |            IP Link               |   Packet  |
      |  Device  +++++ ========================== +++++  Device  |
      |    1      |\                                /|     2     |
      |-----------| \                              / |-----------|  
                     \                            / 
                      |       |-----------|      | 
                      |-------| Photonics |------| 
                              |-----------|   

~~~
{: #figure-correlation title="Correlation between Optical underlay and packet IP links overlay "}

## R3: Support for "Network Visibility" 

The solution shall provide the end-to-end multi-layer "Network Visibility and Visualization" ({{pluggables-operators-requirements}}, Page 5 requirement 1).

This requirement covers not only the network visualization at individual optical or packet layers, but the network visualization across packet and optical layers. 

## R4: Support for "Coherent Plug telemetry data"

The host platform (e.g., packet device) shall provide full access to all telemetry data from the coherent plug. This data shall be streamed to one or more client controller(s) using an appropriate agree protocol and this data shall be provided in a timely manner. The data streamed shall include all alarms, PM reports, PM threshold alerts and state changes (including both dynamic state and config state) supported by the plug. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}

All standard data and all proprietary data from the plug should be made available to one or more controllers by the platform hosting the plug. The platform hosting the plug should not attempt to interpret the plug data prior to making it available to a controller. A generic approach to mapping the data to the interface model should be adopted wherever possible. The data should be made available with no intermediate transformation by the platform hosting the plug. All notifications should be propagated transparently (see R4).

It is recognized that some aspects of the plug, such as electrical power consumption and other parameters, will need to be understood by the host platform control functionality which can help the host to identify degradation/faults in the line and take routing decisions based on that. These properties should be expressed clearly by the plug in a standard, generic and consistent fashion.

## R5: Support for alarms telemetry across packet and optical layers

This requirement mandates the real-time collection of "Alarm Event Notification" telemetry data from both packet and optical layers ({{pluggables-operators-requirements}}, Page 5 requirements 1 and 6).

The solution shall provide:

* Collection of "Alarm Event Notification" for both packet and optical layers
* Alarm correlation across packet and optical layers

## R6: Support for PM telemetry across packet and optical layers

This requirement mandates the real-time collection of performance Monitoring (PM) data from both packet and optical layers ({{pluggables-operators-requirements}}, Page 5 requirements 1 and 6).

The solution shall provide:

* Collection of "performance Monitoring" for both packet and optical layers
* End to end performance management KPI across packet and optical layers

## R7: End-to-end provisioning and deletion of optical services

The solution shall support end-to-end provisioning and deletion of optical services ({{pluggables-operators-requirements}}, Page 5 requirements 2 and 3).

## R8: End-to-end provisioning and deletion of packet services

The solution shall support end-to-end provisioning and deletion of packet services ({{pluggables-operators-requirements}}, Page 5 requirements 2 and 3).

{{figure-e2e-services}} shows a typical packet VPN service between two packet devices. It also shows the multi-layer correlation between packet service and the underlay optical networks. In addition to  provisioning and deletion of VPN services, the solution shall also support the multi-layer visualization of such VPN services.

~~~ 
          <------------------- VPN Service ------------------->
            <-------------- IP/MPLS TE-Tunnels ------------->
              <-- IP link -->               <-- IP link -->
               <---- ES ---->               <---- ES ----> 
                <--- OS ---->               <---- OS --->
                <-OF-> <-OF->               <-OF-> <-OF->

    |--------|                 |---------|                 |---------| 
    | Packet |                 | Packet  |                 | Packet  | 
    | Device +++ =========== +++ Device  +++ =========== +++ Device  |
    |   1    |\               /|   2     |\               /|   3     |
    |--------| \             / |---------| \             / |---------| 
                \           /               \           /
                 \-----|   |                |   |------/
                       |   |                |   |
                 |---------------------------------------|           
                 |    Photonics (ROADM + Amp + Regen)    |
                 |                  +                    |
                 |                xPonder                | 
                 |---------------------------------------|  

  Legend:
    ES     L2 Ethernet Service
    OS     Optical Service
    OF     Optical Fiber
    ====   IP Link
    ----   Optical fibers
    ++++   Coherent pluggables
~~~
{: #figure-e2e-services title="End-to-end Packet Services"}

## R9: Multi-layer assurance across both packet and optical layers

The solution shall support the multi-layer assurance and troubleshooting across packet and optical layers ({{pluggables-operators-requirements}}, Page 5 requirement 5).

## R10: Support operators' realization practices

The solution shall support the operators' realization practices where the functional components for control and management of packet and optical networks might be spread across controller in packet and optical operational centers.

In general, the industry agrees on the functional components that are needed for converged operations: there needs to be a multi-layer controllers that spans both the packet and optical domains in order to synthesize data from both domains and make optimal decisions regarding utilization of assets to deliver high-resiliency and high-performance network services. There is however a difference between packet and optical controllers functional components and their realization – there are different ways service providers can choose to deploy the multi-layer packet over optical controllers including coherent plugs to realize a solution that works in their specific operational environment.

There are several realization approaches including a single control fabric where the optical and packet control functions are deployed in the cloud or simple distinct hierarchy.

## R11: LAG extension

To de added ({{pluggables-operators-requirements}}, Page 5 requirement 6).

## R12: Optical path restoration / protection

Optical path restoration / protection shall be supported ({{pluggables-operators-requirements}}, Page 5 requirement 7).

Depend on the operators' requirements for resiliency on packet and optical networks, some operators prefer to have restoration and protection at optical layer. In these scenarios, to provide the end-to-end full automation across packet and optical network, the automation solution shall integrate the optical layer protection and restoration including expected configurations, assurance, telemetry collection, optimization and path reversion in a uniform fashion.

If an operator deploys an optical protection scheme, the resiliency can be achieved in sub-ms. However, if they deploy a path restoration scheme, the resiliency will not be in sub-ms range.

## R13: Multi-layer control and maintenance operations

The solution shall support the "Multi-layer Control and Maintenance Operations" across packet and optical networks ({{pluggables-operators-requirements}}, Page 5 requirement 8).

To achieve full automation across optical and packet layers, the solution shall support the cross layer control and maintenance operations. In these cases, since the packet and optical layers are inter-dependent (see Requirements R1 above), modifying one layer will impact the services in other layer. For example, if an optical link is disconnected for maintenance, it will impact multiple IP links and packet services. In these cases, the solution shall provide a pro-active approach (using make-before-break scheme) by informing the other layer. This allows the client layers to drain the appropriate IP links, tunnels and packet services and allows graceful maintenance operations across network.

## R14: "Single functional entity" responsible for optical services life cycle management

There shall be a "single functional entity" responsible for optical services life cycle management. The following aspects of optical service life cycle shall be managed and controlled by a single functional entity in the network. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

* Discovery of Optical network functions including coherent pluggables, ROADMs, Amps, Regen, Transponder/Muxponder etc.
* Evaluation of optical services viability
* End-to-end Optical services configuration/modification from plug to plug (or from transponder to transponder).
* Optical services telemetry collection and monitoring performances/faults including the asynchronous notification collected including coherent pluggables.

Note that this requirement addresses the optical control functional aspects but not how they are realized in the network and not how the information needed by the optical controller is collected from the network.

## R15: Support for operators' operational practices 

Existing operators' operational practices on packet and optical network and services shall be supported. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

This requirement emphasizes that the current operator's operational practices such as network planning, commissioning, provisioning, assurance, optimization and protection/restoration for both packet and optical networks shall be preserved whether the optical network is deployed with coherent plugs or with traditional transponder/muxponder. In other words, this requirement emphasizes that the packet and optical control architecture shall deal with any network deployment and administration approaches as coherent plugs are deployed without imposing significant change to the operator's current operational practices. 

There will be significant benefit to operators allowing them to continue to use their existing operational practices to provision and monitor optical services end to end either between transponders/muxponder or between coherent plugs. 

For operators who have specific demarcation between operations of packet network and optical network (with separate physically partitioned controllers) as discussed, it is important that the introduction of converged optical-packet devices does not force a change to their existing operational practices.

As a network evolves, the operational practice may need to change, however, it is clearly always the case that complex photonic networking will require sophisticated dedicated control functions regardless of how the administration is organized.

## R16: Support for multi-layer operational benefits 

The multi-layer packet over optical capabilities and operational benefits among packet and optical controllers such as multi-layer optimization, multi-layer assurance, multi-layer resiliency/protection/restoration and multi-layer planning shall be addressed for full automation in a packet over optical networks. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

To support this requirement, there might be a need for a higher layer controller to collect the configuration and telemetry data from both packet and optical networks and implement various multi-layer operational benefits.

## R17: Support for "greenfield" and "brownfield" networks

The solution shall address both "greenfield" and "brownfield" networks. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

## R18: Optional higher level controller 

Higher level controller shall be optional. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

In some packet over optical networks, the higher level controller might not be needed, depending upon the supported use-cases in that network. Forcing the addition of a higher level controller makes the deployment more costly and potentially more complex. 

## R19: Support of both plugs and Transponders/Muxponders (inc. Regens)

The solution shall support a packet over optical network which contains mix of plugs and Transponders/Muxponders (inc. Regens). See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

Many optical services will have a coherent plug in a packet device at one end and a coherent plug, or coherent optics on some other circuit pack type, in a non-packet device (e.g., storage, application platform, optical regen) at the other end. The solution shall support all current and expected configurations in a uniform fashion.

## R20: Various existing YANG Data Models shall be accommodated

The solution shall enable the use of various existing YANG data models. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

Currently used to configure/monitor coherent transponders (e.g., OpenConfig, IETF etc.), for configuration/monitoring of coherent plugs in packet devices. 

Note that possibly expand (new requirement) to indicate that the YANG data model MUST define all the optical parameters to be exchanged (e.g., power setting) between the network elements and the control and also emphasize access between the plug and device along with necessary mapping neutrality etc. (this was derived from draft-ietf-ccamp-dwdm-if-mng-ctrl-fwk-13).

## R21: Clear demarcation for holistic control of optical network

Holistic control of optical network shall follow clear demarcation. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

Where there is network technology based responsibility partitioning, the controllers should abide by the technology boundaries. The packet controller shall control packet functions and the optical controller shall control optical functions. The optical technology includes coherent terminal functions and hence these shall be controlled by the optical controller. The packet controller shall not need to be exposed to coherent plugs optical attributes. Optical technology is a separate, distinct and complex technology from packet technology.

## R22: Support for urgent optical control actions 

Urgent optical control actions shall be supported in a timely manner. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

During some of the operation and restoration/protection cycles of the converged packet and optical networks, urgent action on the configuration of the pluggable may be required where the decision to take the action and the action detail are the responsibility of the optical controller. For example, during the restoration and protection of the Optical services, there might be a need for re-tuning and re-coloring of optical services. This involves changes in both the coherent plugs and ROADM networks. 

## R23: Minimize fragmentation of optical parameter provisioning

The solution shall minimize fragmentation of optical parameter provisioning. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

It is highly beneficial to closely coordinate configuration parameter settings across the optical network including pluggables as inconsistent configuration can potentially cause disruption to other photonic paths.

## R24: Direct path to relevant controller

Network information shall take direct path to relevant controller. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

It shall be possible to access all configuration information and telemetry data available from the coherent plug as directly as possible (ideally with no intervening transfer delays).

## R25: Evolution to expected future controller deployment approaches

Evolution to expected future controller deployment approaches shall be supported. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

The solution shall be designed to provide a clear evolution path to the probable future architecture (which is expected to be focused on disaggregation of control). In this architecture it is expected that control components with specific focused functions will have direct access to the corresponding functions in target systems and that asynchronous and simultaneous access to these functions will be vital.

## R26: Evolution to future packet processing deployment approaches

Evolution to future packet processing deployment approaches shall be supported. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

The solution shall be designed to provide a clear evolution path to support control of packet and optical functions deployed using emerging strategies (e.g., virtual routers, cloud based functions) where the network functions are not constrained by physical boundaries. Operational approaches native to these environments should be supported. 

## R27: Support for extensible control architecture

The control architecture shall be extensible. See {{draft-davis-ccamp-photonic-plug-control-arch-02}}.

The solution will allow addition of new capability whilst operational where that capability may be vendor specific, technology specific, application specific or generic and where the addition may be of a new version of an existing function etc.

# Acknowledgments
{:numbered="false"}
