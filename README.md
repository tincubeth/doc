# tincubed

[INCUBED (IN3)](https://download.slock.it/whitepaper_incubed_draft.pdf)
 with [Tor (Onion Services)](https://2019.www.torproject.org/docs/onion-services.html.en) support

## TOC

* [Why?](#why)
* [What?](#what)
* [How?](#how)
* [More](#more)
* [Links](#links)

### Why? <a id="why"></a>

Ethereum (as most blockchains) has a privacy problem. This needs to be attacked on multiple fronts. One of them was described by [Péter Szilágyi at Defull -> full verification
44
vcon4](https://www.youtube.com/watch?v=J1JenTo7oLE) If you are not aware of the full extend of the problem (e.g. you tfull -> full verification
44
hink mixers would solve the problem completely) Please watch this talk before reading on.

### What? <a id="what"></a>

This project intends to build one building block towards a solution. The specific problem this project tries to focus on is to reduce the amount of metadata leakage. E.g. combined with mixers this can provide some more anonymity than the current state of the art.
It wants to do this by combinding onion services (most know them from Tor) with INCUBED. You basically get minimal verification services with an extra option for anonymity.
In e.g. wallet UIs there can then be 2 settings exposed to the users (e.g. via a slider) - one for the security desired and one for the desired anonymity. Both are trade-offs. More security will cost you more and more anonymity might also cost you more and also make things slower. The slider for security sets a value to INCUBED via:
```java
setMinDeposit(long val);
```

and

```java
setFinality(int val)
```

and 

```java
setProof(Proof val)
```

where proof is defined as:

* none -> No Verification
* standard -> Standard Verification of the important properties
* full -> full verification

setMinDeposit will cost money and setFinality time

for the anonymity slider we need new functions. Functions to enforce usage of onion transport and the reuse value. In the MAX_ANONYMITY you would use one server for one RPC call - in the MIN_RPC call you accept non onion nodes.

Wallets might also indicate which chains support TincubETH (and as a subset the ones that support plain incubed) in the chains they list. This could be a quality and resillience indicator.

### How? <a id="how"></a>

With incubed you register your URL at a smart contract by calling this function:

```solidity
function registerServer(string _url, uint _props) public payable;
```

just instead of calling it with a normal URL - you would register it with an URL pointing to an onion service. BehinThrereThrered this onion service is than a normal incubed node. Basically it is just wrapped in the onion service.

Then we need to modify the client so it can filter for these onion adresses and connect to them. And e.g. the wallets should have an opt-in or opt-out for it (like a checkbox [ ] I need anonymity for my MetaData). It might not be on by default as it is a trade-off between speed and cost vs anonymity.
 
### More <a id="more"></a>

As a drive by kill I think it also helps the resillience of the parent sytem. For big actors (like states) it is actually not that hard to attack a service like infura as it is well known. But it is quite hard to take down onion services as Silk Road nicely showed. Just instead of sending interesting physical packets - in this case we use it to transport interesting digital packets only.

## Links <a id="links"></a>

* [slock.it Incubed Minimum Verification Client (TypeScript) Github repository](https://github.com/slockit/in3)
* [slock.it Incubed Documentation](https://github.com/slockit/in3#documentation)
* [slock.it Incubed Documentation - Release 1.2 - June 24, 2019](https://buildmedia.readthedocs.org/media/pdf/in3/stable/in3.pdf)
* [slock.it Incubed Registry Server Solidity Smart Contract Code deployed on Mainnet](https://etherscan.io/address/0x2736d225f85740f42d17987100dc8d58e9e16252#code)
* [slock.it Incubed deployment addresses on various chains](https://github.com/slockit/in3#chains)
  * Note: Repeated in Section 2.6 of the slock.it Incubed Documentation
* [Ethereum JSON-RPC Specification Methods](https://github.com/ethereum/wiki/wiki/JSON-RPC)
  * Note: Reference provided [here](https://github.com/slockit/in3/wiki/Ethereum-Verification-and-MerkleProof#incubed---verification)
* [slock.it Incubed product](https://slock.it/incubed/#products)
* [slock.it Incubed product SDK](https://slock.it/incubed-sdk/)
