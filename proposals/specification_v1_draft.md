# DeCert Initial Specification Proposal
This document is intended to remain agnostic to implementation details such as how information will be stored.

## Objective
DeCert (decentralized certification) is a project aimed to provide a framework for parties to securely attest to information for external parties to privately view.

## Use cases
A health inspector inspects a restaurant and approves it. She publishes a certificate that the restaurant passed inspection. The certificate includes what the inspection covered, when it occurred, and various information to identify the restaurant, such as the coordinates of the restaurant, identifier of the property, management's identity, and a picture of the outside.
The restaurant prints a copy of the certificate with a QR code which a visitor could scan with their phone to see the digital certificate and confirm its validity. Trust of the inspector is not addressed in this example.

TODO: add a couple more examples

## Threat model
TODO

## Design goals
Certificates should optionally be able to be distributed without revealing confidential information on the certificate whenever shared.

Identities which certificates are managed by should be dependably persistent. Identities shouldn't be lost or compromised because a single person lost their phone. Upon lost identity, effective mitigations should be convenient.

Any conditions regarding mutable or hidden information should be understood by anyone seeing a certificate.

## Design
Nothing published can be directly modified. 
Only an updated copy can be published. 
The timestamps of publishes should be trustworthy so that state can be reliably inferred for any past instant.

### Certificate structures
Every certificate must fit a published structure. 
Structures enable machines to tell if they can compare and list apples-to-apples, and they help humans ensure consistency. 
Structures list all fields forming a certificate. 
Human-readable descriptions of any fields may be included. 
Machine-readable constraints of any fields may be specified. 

Any field may be marked to be distributed separately, the main certificate only carrying the confidential field's content's salted hash. The salt is since the hash may be used to find the content already (like on IPFS). 

Structures may provide template or mandatory permissions. These include terms for updating fields and updating permissions. 

Structures may inherit parent structures. Children must contain all of their parent's fields and permissions, and they may add fields. This way certificates with different structures but a common parent can still be operated on like the parent, allowing structures to be expanded without becoming backwards-incompatible. 

### Identities
Identities are used to dictate what parties created and have permission to modify other identities and certificates. 
Individuals might have identities managed by keys. 
Organizations or job-positions should probably be managed by other identities.

Identities contain permissions for signing certificates, a whitelist (or * wildcard) for structures that can be signed, terms for active and retroactive revocation, and permissions for changing these permissions

Identities can be revoked and possibley marked invalid since a certain time in the past in case a compromise goes unnoticed.

### Certificates
Certificates say who (plural or singular) created the certificate.  
TODO: is there anything left to say here?

### Permissions
Permissions are defined by what object(s) the permissions are being defined for, what actions concerning the objects are being allowed, and which actors (identities/keys) need to sign-off the action. Actors are each assigned a weight. A weight threshold is defined which must be met before the action can be validly completed. The weight of the signers must meet or exceed the threshold. 
Every action traces to identities which all trace to keys. 
Before enough signatures are made, changed object and signatures can be put in a staging area for user convenience instead of requiring an out-of-band method for compiling signatures.

#### Identity permissions
Who can action [create/update cert[structures|*]|create/update IDs?|*]

Who can alter permissions?  
*specifics*

#### Certificate permissions
Which fields can be updated by whom?

Who can update permissions?


### Signing and distribution
Everything theoretically can be signed, distributed, and verified offline. However, maintaining this system will become difficult as the web of identities needed to verify a certificate expands. Staging for signatures and publishing (and maybe hosting on something like IPFS) once signatures are received could be a SaaS to fund raise for development. Skycoin or Maidsafe could be distribution platforms instead.

## API
TODO

