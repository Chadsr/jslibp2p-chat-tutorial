Peer Identity
=============

One of the key concepts of libp2p is how the identity of a peer is established.  We talked about multiaddresses in the previous section which tell libp2p how to connect to a specific node and the critical data element that uniquely identifies a node is it's [`PeerId`](https://docs.libp2p.io/concepts/peer-id/).  Each libp2p has a secret, private key along with a corresponding public key that can be shared with other peers on the network.  This key pair is what enables libp2p nodes to communicate securely. The PeerId is a cryptographic hash of the node's public key.  There are several key types that can be used and the details are found in the [PeerId spec](https://github.com/libp2p/specs/blob/master/peer-ids/peer-ids.md).

When setting up a libp2p node, you provide an `options` object to the `libp2p.create` function that tells libp2p what modules you are planning to use and can also provide additional configuration details as well.  Importantly, you can tell libp2p what your node's PeerId is as well as specify what addresses you want your node to listen on with code like below:
```
const node = libp2p.create({
    addresses: {
        listen: ['/ip4/127.0.0.1/tcp/0']
    },
    peerId: {
        "id": "Qma3GsJmB47xYuyahPZPSadh1avvxfyYQwk8R3UnFrQ6aP",
        "privKey": "CAASpwkwgg...",
        "pubKey": "CAASpgIwggEiMA0G..."
    }   
})
```

When your node connects to other peers on the network, you can access their public keys and multiaddrs from the `connectionManager` methods and then store them in a `peerStore`, which contains all the connection/protocol data node needs to communicate, including known peers, supported protocols, etc.  All of the peerStore functions can be found here in the [js-libp2p docs](https://github.com/libp2p/js-libp2p/blob/master/doc/API.md#peerstoreaddressbookadd)

* Try it yourself, 
    - Modify on start listener such stat it prints all the mutiaddrs
    - Add a new listener for connection:peer (https://github.com/libp2p/js-libp2p/tree/v0.25.4#libp2ponconnectionstart-peer--) documentation for checking the call back
    - In the callback of the litener, use the peerinfo and print the peer id in string 
* Run it locally, what do you see?
    - List of your connection multiaddrs

<!-- tabs:start -->

#### ** Template **

[embedded-code](../assets/2/2.1-template-code.js ':include :type=code embed-template')

#### ** Solution **

[embedded-code-final](../assets/2/2.1-finished-code.js ':include :type=code embed-final')

#### ** Previous Chapter Solution **

[embedded-code-previous](../assets/2/2.0-finished-code.js ':include :type=code embed-previous')

<!-- tabs:end -->
