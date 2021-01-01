# Authentication & Ownership

**Authors:  *Jubin Jose*, *Nibin Peter***



All the `API interactions` and `data operations` in Aquila DB and across Aquila Network (directly or indirectly) is [`"Authenticated"`](https://en.wikipedia.org/wiki/Authentication) and most of them is then recorded as a `transaction log` along with the [`proof of "ownership"`](https://en.bitcoin.it/wiki/Proof_of_Ownership). `"Authentication"` is usually completed followed by an [`"Authorization"`](https://en.wikipedia.org/wiki/Authorization) of the identity.



Aquila Network enables All three - Authentication, Authorization and ownership elegantly by enabling [DID](https://en.wikipedia.org/wiki/Decentralized_identifiers) and assumes each DID as a separate [agent](https://en.wikipedia.org/wiki/Agent_(economics)). It is open to any DIDs as long as a unique identifier is supplied as identity URI (base-58 string) along with proof (base-58 string) of ownership over performed operation. And this identity proof should be validated externally with a service which is obvious and accessible to all concerned nodes in Aquila Network.



>  DIDs compatible with Aquila Network is supposed to grow over time with additions and deprecation. Currently, the specification is compatible with `RSA` and `ECDSA` based DIDs only.