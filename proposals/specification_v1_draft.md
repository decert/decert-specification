# DeCert Initial Specification Proposal
## Objective
DeCert (decentralized certification) is a project aimed to provide a framework for parties to securely attest to information for external parties to privately view.

## Use cases
A health inspector inspects a restaurant and approves it. She publishes a certificate that the restaurant passed inspection. The certificate includes what the inspection covered, when it occured, and various information to identify the restaurant, such as the coordinates of the restaurant, identifier of the property, management's identity, and a picture of the outside.
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
Machine-readable contraints of any fields may be specified. 
Any field may be marked to be distributed separately, the main certificate only carrying the confidential field's content's signature.

?May template or mandatory modification terms be included in structures? 
... Nah. Future certificates could specify preceding certificate that they mean to supercede. 
... Nah to the nah. The structure or old certificate could specify on what terms supposed superceding certificates are valid.
Perhaps some manner of child strctures should be allowed so that common fields from a common parent can be compared, but additional details can be added without needing to create a completely backwards-incompatable structure.

### Identities
Identities are used to dictate what parties created and have permission to modify other identities and certificates. 
Individuals might have identities managed by keys. 
Organizations or job-positions should probably be managed by other identities.

Identities contain permissions for signing certificates, a whitelist (or * wildcard) for structures that can be signed, terms for active and retroactive revocation, and permissions for changing these permissions

Identities can be revoked and possibley marked invalid since a certain time in the past in case a compromise goes unnoticed.

### Certificates
Notes: hidden fields. Perhaps they only contain salted hash of field content and content is distributed seperately.

### Permissions
Notes:
objects actions actors[[identities or keys, weight], threshold weight]
every action traces to identities which all trace to keys
perhaps before enough signatures are made, changed object and signatures can be put in a staging area for user convenience instead of requiring an out-of-band method for compiling signatures.

## API
TODO

