# **Client-Server Architecture**
- a computing model where multiple components work together to communicate, AKA networking computing model (because all the services and requests are delivered over a network)
- considered a form of distributed computing system because the components are doing their work independently of one another
- server acts as the producer and client act as the consumer; server provides high-end, computing-intensive services to the client on demand (appliation access, storage, file sharing, printer access, server's raw computing power)
- server hosts, delivers, and manages most of the resource and service to be consumed by client
- client computers are connected to a central server over a network or internet connection
- a server can manage several clients simultaneously, and one client can connect to several servers at a time
## **Downsides**
- more vulnerable to unpredictable workloads
- vulnerable to DDoS attack, as client-server model wasn't set up for thresholds above a certain amount of traffic (allowing out-of-control client activity swamps a server)

## **Peer-to-Peer Architecture**
- a decentralized computing model where each workstation, or node has the same capabilites and responsibilites, commonly used for content distribution
- may also be used to refer to a single software program designed so that each instance of the program may act as both client and server, with the same responsibilities and status
- p2p network distribute the workload between peers, all peers contribute and consume resources within the network without the need for a centralized server
- works best when there are losts of active peers in the network, new peers joining can easily find other peers to connect to
- less peers means less resources available overall, eg: in a p2p file-sharing application, the more popular a file is, means lots of peer are sharing the file, the faster it can be downloaded
- p2p works best if the workload is split into small chunks that can be reassembled later, that allows a large number of peers to work simultaneously on one task and each peer will have less work to do, in the case of file-sharing, the file can be broken down so peer can download many chunks of the file from different peers at the same time
## **Advantages**
- no central server to maintain, no need of network operating system, more economical
- no single point of failure due to decentralized nature, unless the network is very small
- resilient to change in peers, if one peer leaves there is minimal impact on the overall network, if a large group of peers joined the network can handle the increased workload easily
- can survive cyber attacks easily as there is no centralized server
- Scalability - the network is very easy to scale up
- Efficiency - the network uses available resources of peers, who normally wouldn’t
contribute anything in a typical client-server architecture
- Adaptability - the network can be used for a variety of use cases, and it can easily
start up another network if one is taken down, which means there is no single point of
failure

## **Downsides**
- if one peer is infected with virus and uploads a chunk of file that contains the virus, the virus gets spread quickly to the other peers
- if too many peers in the network, difficult to ensure they have the proper permissions to access the network if a peer is sharing a confidential file
- contain freeriders or leechers, users who utilized resources shared by other ndoes, but do not share anything themselves, will be a threat if utilized to facilitate illegal and immoral activities