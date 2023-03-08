# Networking

## Gateway and Broadcast

Two address are reserved in a network.

- Address 0 is reserved to be used by the network gateway (how to access outside of the network)
    - `192.168.1.0/24`
- Address 255 is reserved to send broadcast messages to all nodes in the network.
    - `192.168.1.255/24`

## Subnet Mask Binary Shorthand

- `192.168.1.1/24`
    - valid 192.168.1.0 - 192.168.1.255 (subnet mask is 255.255.255.0)
- `192.168.1.1/32`
    - valid 192.168.1.1 only (subnet mask is 255.255.255.255). This node can only talk to itself and the default gateway. Used for loopback, machine isolation, and webservers (multiple sites bound to a specific IPv4 address).
- CIDR - Classless Inter-Domain Routing

# Network Layers

## OSI (Open Systems Interconnection) Model

- Layer 7 – **Application**: application protocols like HTTP, SSH and SMTP
- Layer 6 – **Presentation**: character encoding like ASCII vs UTF-8
- Layer 5 – **Session**: mechanisms for establishing point-to-point communication
- Layer 4 – **Transport**: data transfer protocols like TCP and UDP
- Layer 3 – **Network**: network routing protocols like IP and OSPF
- Layer 2 – **Data Link**: protocols that connect the physical layer to the network layer, such as Ethernet and ARP
- Layer 1 – **Physical**: the physical components such as cable wiring and Wi-Fi

## TCP/IP Model

- Layer 7 – **Application**: application protocols like HTTP, SSH and SMTP
- Layer 4 – **Transport**: data transfer protocols like TCP and UDP
- Layer 3 – **Network**: network routing protocols like IP and OSPF
- Layer 2 – **Data Link**: protocols that connect the physical layer to the network layer, such as Ethernet and ARP
- Layer 1 – **Physical**: the physical components such as cable wiring and Wi-Fi

# Architecture

## Spine-and-Leaf

TODO

# Switches

## Fabric Switch

TODO

## ToR (Top of Rack) Switch

TODO

# CIDR (Classless Inter-Domain Routing)

TODO
