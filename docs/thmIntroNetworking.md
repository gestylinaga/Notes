# Introductory Networking

## The OSI Model -- Open Systems Interconnection

* 7 layers: **A**nxious **P**ale **S**hakespeare **T**reated **N**ervous **D**runks **P**atiently
    
    - Application -- layer 7

        + provides networking options for programs on a computer

        + lets applications transmit data

        + when data hits this layer, it's passed down to the presentation layer

    - Presentation -- layer 6

        + receives data from application layer; data not in standardised format

        + this layer translates the data, handles any encryption/compression/or transformation

        + when data formatting is complete, it passes to the session layer

    - Session -- layer 5

        + attempts to connect to remote computer; else process stops here

        + if succesful: maintain connection w/ session layer of remote computer

        + creates unique 'session' to allow multiple requests w/out mixup

            * like multiple tabs in a browser

        + when succesful connection is made, data passes to the transport layer

    - Transport -- layer 4

        + chooses which protocol to send data over

            * TCP -- Transmission Control Protocol

                - 'connection-based' -- connection is established and maintained for duration of request

                - reliable; ensures *all* packets get to right place

                - acceptable speeds, re-send data if necessary

                - accurace over speed: file transfer, loading a webpage

            * UDP -- User Datagram Protocol

                - opposite of TCP

                - packets are 'thrown' at target computer

                - keeping up is remote computer's problem

                - think Skype, how video quality degrades with connection quality

                - speed over accuracy: video streaming

        + with protocol selected, data is divided into pieces for easier transport

            - *segments* over TCP

            - *datagrams* over over UDP

    - Network -- layer 3

        + responsible for locating destination for request

        + *Logical* addressing -- IP addresses

            - IPV4: 192.168.1.1 -- common home router address

    - Data Link -- layer 2

        + focuses on physical addressing of the transmission

        + receives packet from network layer -- including IP address of remote computer

        + adds physical MAC address of reveiving endpoint

            - NIC -- Network Interface Card -- inside every network enabled computer; holds MAC address

            - MAC -- Media Access Control -- unique physical address of a computer; can't be changed; can be spoofed

        + presents data in suitable format for transmission

        + when receiving data: checks for corruption (possible in layer 1: physical)

    - Physical -- layer 1

        + computer hardware level

        + electrical pulses that make data are sent and received here

        + converts binary data of transmisson into signals to send over network

        + receives incoming signals and converts them back into binary data

### Encapsulation -- process by which data can be sent from one computer to another

* as data passes through layers, information is added to transmisson

    - IP addresses from Network layer

    - protocol type from Transport layer

    - data link adds piece onto the end to ensure no corruption after receiving

    - added bonus security, transmisson can't be tampered with

* data referred to as 'segments/datagrams' in L4

* data referred to as 'packets' in L3

* data referred to as 'frames in L2

* data broken down into 'bits' by L1

* De-Encapsulation -- process is reversed in receiving computer


## The TCP/IP Model

* similar to OSI model, but four layers:

    - Application -- layer 4

    - Transport -- layer 3

    - Internet -- layer 2

    - Network Interface -- layer 1

> sometimes 5 layers, breaking Network Interface down into:
>
>> Data Link
>> 
>> Physical layer
>
> accepted and well-known but not officialy defined yet

* in TCP/IP, Application layer matches top 3 layers of OSI model

* Network Interface layer covers bottom 2 layers

* TCP -- Transmission Control Protocol

    - controls flow of data between two endpoints

* IP -- Internet Protocol

    - controls how packets are addressed and sent

* **3-Way Handshake** -- before sending data over TCP, the formation of a stable connection between 2 computers

    1. SYN -- synchronise; request sent to remote server to initialise a connection

    2. ACK -- acknowledgement from server, along with original SYN sent back to client

    3. Client sends ACK back, confirming succesful connection

    - any lost data is re-sent, seeming lossless

## Basic Networking Tools

* Ping -- test possible remote connections

    - returns IP address instead of URL

```
ping <target>
ping google.com
```

```
ping muirlandoracle.co.uk
217.160.0.152
```

* Traceroute -- maps the path requests take to target machine

    - flag -i to force interface: VPN/ethernet/wireless
```
traceroute <destination>
traceroute tryhackme.com
```

* Tracert -- traceroute for windows
```
tracert <destination>
```

* WHOIS -- queries who a domain name is registered to

    - [web version of WHOIS](https://www.whois.com/whois/)

    - may not be insalled by default

```
whois <domain>
```

> DNS -- Domain Name System
>> special server that returns IP addresses from URLs
>
> Recursive DNS servers
>> owned by companies like Google and OpenDNS or your ISP
>>
>> maintain cache or popular results
>
> Root name servers
>> exactly 13 in the world
>>
>> redirect requests deeper to TLD servers -- Top-Level-Domain servers
>
> TLD -- top-level-domain servers
>> 1 for handling .com addresses
>>
>> 1 for handling .co.uk addresses etc...
>>
>> passes down to Authoritative name servers
>
> Authoritative name servers
>> handle domains directly
>>
>> every domain in the world has its DNS stored on one

* Dig -- does the above, manually

    - ANSWER section obviously important

    - TTL -- Time To Live -- lifespan of local cache, measured in seconds

```
dig <domain> @<dns-server-ip>
```

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
