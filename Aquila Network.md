# Aquila Network Overview

Aquila Network in a nutshell is a "decentralized self organizing information discovery and service layer".

 

**Overview of the space**: With latest advancements in decentralized computation, the edge first design is becoming the new norm for achieving scalability and availability. Explosion of new protocols and virtualization (ex: [EVM](https://ethereum.org/en/developers/docs/evm/), [OCI](https://opencontainers.org/), [LXC](https://linuxcontainers.org/)) techniques that allow platform agnosticity ensures inclusion of wide range of dynamic, independent compute resources across the globe. On top of this, research and developments involving realtime social experiments in carefully designed game theoretic token economics promises self sustainability of these networks through emergent cooperation.



When we look at developments in this space, a lot of activity and progress is happening in peer to peer networking as well as data storage (ex: [IPFS](https://awesome.ipfs.io/), [SWARM](https://swarm.ethereum.org/), [Hyper](https://hypercore-protocol.org/)). However, there's a thin layer sandwitched in between storage and network layer which needs to be developed as the space grows. This thin layer takes care of organization and discovery of information. At the end of the day, this layer is essential to extract real value from bottom data layer and is driven by the network layer above it.



Aquila Network's design philosophy is "**simplicity and reusability**". It is designed in a way to embrace the very fundamentals of technology and fine tune to make the modules even simpler, iteratively. Aquila Network never reinvents the wheel, if not necessary. This is to reduce transition cost for everyone.



Aquila DB is at the core of everything in Aquila Network. Every other module is connected to Aquila DB directly or indirectly. There are three types of modules based on their connected relationship with Aquila DB. 

- Data layer module

  [ External data storage (IPFS, SWARM, ...) ] <===> [ Data layer module ] <===> [ Aquila DB ]

- Network layer module

  [ Aquila DB ] <===> [ Network layer module ] <===> [ Network layer (Couch, Ethereum, IPFS) ]

- Interaction layer module

  [ User ] <===> [ Interaction layer module ] <===> [ Aquila DB ]

  or,

  [ Aquila DB ] <===> [ Interaction layer module ] <===> [ Aquila DB ]



*Aquila Network in the space*

![Aquila Network layers](https://user-images.githubusercontent.com/19545678/102682533-40cc0100-41f0-11eb-9810-a9d7851dc144.jpeg)