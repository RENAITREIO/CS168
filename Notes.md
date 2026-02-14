# CS168 Notes

## Intro
### Layers of the Internet
internet design challenges
- fedoration
- scale
- evolution
- diversity
- asynchrony
- fault tolerance

protocol
- syntex
- semantics

layer 1 - physical(moving bits across space)  
need some phisical technology

layer 2 - link(local networks)  
links between machines  
exchange packets

layer 3 - internet(connecting local networks)  
the Internet is a network of networks  
end hosts: machines  
switches(aka routers): receive packets and forward them toward destination  
modularity  
layer 3 offers a best-effort service model  
not promissing success

layer 4 - transport(reliably deliver packets)  
thinking about flows(aka connections)

layer 7 - application(implement services)

> The session layer (5) was supposed to assemble different flows into a session (e.g. loading various images and ads to form a webpage), and the presentation layer (6) was supposed to help the user visualize the data. Today, the functionality of these layers is mostly implemented in Layer 7.

headers  
packet needs some extra metadata  
packet = headers + payload

multiple headers

end hosts implement all the layers  
rounters only implement layers 1-3

### Design Principles
1. decentralized control  
    alternative: SDN, DSDN
2. best-effort services model  
    alternative: introduce "quality-of-service" guarantees
3. route around trouble
4. dumb infrastructure(with smart endpoint)  
    alternative: routers look inside to detect attacks
5. end-to-end principle
6. layering  
    alternative: protocols spanning multiple layers to optimize
7. federation via narrow-waist interface

the narrow waist: IP(internet protocol) is the only protocol at layer 3

demultiplexing:  
layer 3: add header field tell what the next layer protocol is  
layer 4: add a port number  
private client use randomly-generated port number  
public server must use a fixed, well-known port number

logical port and physical port

implement layers in the end host  
layers 1 and 2 are implemented in hardware, on the network interface card(NIC)  
layers 3 and 4 are implemented in software, in the operating system  
layer 7 is the applications running in software

end-to-end principle: certain application features(e.g. reliability) must be implemented at the end host for correctness  
it's not an unbreakable rule

designing resource sharing  
- static allocation(fixed)
- statistical multiplexing(dynamic)
    - circuit switching(reservations)  
    used in limited settings
    - packet switching(best-effort)  
    default

### Links
properties of a link
- bandwidth  
    measured in bits per second(bps)
- propagation delay  
    measured in seconds
- bandwidth-delay product: bandwidth x delay  
    "capacity" of the link

overloaded links
- transient overload  
    maintain a queue of packets
- persistent overload
    drop packets  
    upgrade router or tell the sender to slow down

packet delay = transmission delay(packet size / bandwidth) + propagation delay + queuing delay

## Routing
### Principle
full-mesh topology doesn't scale well, but high bandwidth  
single-link topology  
network graph is constantly changing  
routing protocols is distributed

- intra-domain routing protocols(interior gateway protocols(IGPs))
- inter-domain routing protocols(exterior gateway protocols(EGPs))
    the Internet use BGP

in pratice, the lines between intra and inter are blurred

destination-based forwarding  
depend on the destination field of the packet  
router keeps a mapping table

forwarding(deliver packets) vs. routing(fill tables)

a global routing state is valid if and only if there are no dead ends and no loops

directd delivery tree  
oriented spanning tree






disc01  
ping, traceroute and dig  
ip time-to-live(TTL)  
internet control message protocol(ICMP) (built on top of IP)
