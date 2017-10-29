
## Module diagram
TODO

## Design assumptions

### Not like Camlistore
The opposite of [Camlistore's assumptions](https://github.com/camlistore/camlistore/blob/master/doc/overview.txt) while still agreeing with [Camlistore's principles](https://github.com/camlistore/camlistore/blob/master/doc/principles.md):
1. diskspace is limited _in practice_
2. bandwidth is metered
3. CPU feels too slow
4. people can't safely store private keys

### Additional assumtions
5. battery juice is precious
6. someone is watching and storing all connection metadata on internet and other public networks
7. democracy and freedom maybe won't last
8. unfiying filesystems and naming is hard
9. once a something is shared, or viewed in public, don't rely on it still being private (analog loopholes, targeted crypto analysis and XOR) 

## Goals (measurables)
- store only data you care about (disk usage(private fullsync allspan instance) <= disk usage(same data minus allspan's added functionalities and underlying data)
- nibmle (<10 kLOC)
- standards compliant (prefer tools and protocols with semver ">=1.0")
- automatic and adhoc naming (user can define part of the name, but isn't forced to resolve naming conflict. Adding (1) or (Copy)is technically allowed here, but frowned upon)
- anonymity (leak less metadata than if you'd be using Signal chat app)
- incremental sharing (adding a participant can't disrupt previous users)
- data integrity (verifiable chain of custody of file metadata, which verifiably matches the covered data)
- (partial) recoverability of data referenced in my non-private indexes also if my private key for the metadaa and my decryption keys are lost (local index has references which can be matched to willing participants, enabling data arhaeology or recovering photoalbums)

## Stretch goals (measurables)
- dead mans switch (a user who's not routable - i.e. offline - for a defined time triggers release of some decryption keys)
- recreate lost decryption keys (reset or recreate user secrets from userfile-at-rest and saved recovery phrase)
- burn a previous i.e. exposed gestalt key (a gestalt revocation message can be published)
- integration with messengers and social walled gardens (maybe a browser extension that snaps up any postsed text and media)
- device independent (an allspin user can use all functionality via a public computer on an untrusteed open network. Visual/audio for ex/infil of data through the untrusted device is allowed)
- managed diska space (data is deduped, avoiding storing widely high bandwidth-available public data, and/or farming out storage to friends and paid storages)
- [sousveillance](https://github.com/allspan/allspan/blob/master/docs/uses/sousveillance.md) (some minimal lifestream data can be insta-shared from one user to another)

## Differences to related _open_ solutions
* [Camlistore's design](https://github.com/camlistore/camlistore/blob/master/doc/arch.md) gives you a server or service-based storage solution to last a lifetime, with considerations for not complicating future data arhealogy. Do read it's full [raison d'ètre](https://github.com/camlistore/camlistore/blob/master/doc/overview.md)
* [Upspin](http://upspin.io) is a global naming solution for files and users, meant to be usable across online services and walled garden social platforms.
* [Hashbackup](http://www.hashbackup.com/home/features) is Dropbox minus the sharing, and likely feature completed.
* (Diaspora*)[https://wiki.diasporafoundation.org/Architecture_overview] is a good data transport, but routing is federated. Profile, sharing etc was _initially_ designed very close to something Allspan could be built on top of. It ticks many boxes, but requires trusted system operators.

## Solution topologies
Allspan wants to have multiple independent clients, finding their data through locally stored (and normally safely backed up) collections of keys and metadata, not requiring servers, potentially piggybacking on any and all possible storage options available, paying passage or hustling along.

Contrast that with the alternatives, none of which have a payment or tipping method integrated:
- Upspin has a client, a directory server and storage servers: https://github.com/upspin/upspin/blob/master/doc/images/arch/overall.png
- Camlistore has a server (frontend) per user, and many storage servers: https://github.com/camlistore/camlistore/blob/master/doc/arch.md
- Diaspora* has one server (pod) per several users
- freenet has P2P gosspi-flooding. All participants are equal, except a few, who may have superpowers.
- Napster / DirectConnect / EMule are public, centralised with optionally obfuscated physical location central directories, and clients are qeual
- BitTorrent is P2P file distribution with optional VPN-obfuscation of identity, with peer-supplied Tigerhash routing of torrent pieces

## Useful technologies
- signed, traceable chain of claims, built like https://help.github.com/articles/signing-commits-with-gpg/
- [SQRL](https://www.grc.com/sqrl/sqrl.htm) for Gestalt keys, and possibly to help people store private keys
- [Snappy compression](https://google.github.io/snappy/) for cpu-friendly space/&time saving
- private long-term routing by [paid remailers](http://nakamotoinstitute.org/for-pay-remailers/)
- nodejs or https://github.com/twisted/twisted asynch runtimes
- [multihash](https://github.com/multiformats/multihash), ([multibase](https://github.com/multiformats/multibase), etc


## Prior art in a wide sense
- What's at https://github.com/camlistore/camlistore/blob/master/doc/prior-art.md
- All mentions under [Diff. to realted solutions](https://github.com/allspan/allspan/blob/master/docs/arch.md#differences-to-related-open-solutions)
- File sync and dropbox services
- [Android Syncbase](https://vanadium.github.io/syncbase/) is offline-first P2P backup.
- storing and sharing solutions; FreeNet, Gnutella, Napster, BitTorrent, tor, i2p, IPFS, Storj, Sia
- social networks, and Diaspora*, Identi.ca, Voat, etc

## Important processes (protocol)
To be defined:
- finding routes
- offering blobs
- sharing metadata
- fetching a file

## Security
- Use only battle hardened crypto and in the same way as it's used elsewhere by bigger targets. Compare Bitcoin SHA256 and EC.
- E2E and encrypted-at-rest


### Access control
Once something is shared, you can practically no longer control it.

Uncareful file leaking could possibly be detected by tracking downloads, or searching external indexes to check if it has leaked, decreases anonymity since you must send both the question and get the answer, likely many times. Any contract based tracking can't be enforced.

, or check 3rd party indexing services if they've found out about the files existence or popularity, but analogous to looking at the bitcoin adresses

Some very unreliable tracking of how a shared file spreads can be possible from scouring 3rd party indexes, or just tracking downloads of the metadata and blobs from the places where you uploaded it to. Any tracking attempts though will weaken your anonymity, analogous to how this works with bitcoin.

 we have that someone who can download and decrypt a file, could as well keep the access to that file forever. Having lists of who was given access to what is not really trustable, especially since someone might catch the blobs and someone else get the decryption keys. Or just the metadata, and from there find the referenced data from other, more leaky, storage systems.

Compare https://github.com/upspin/upspin/blob/master/doc/security.md and https://github.com/upspin/upspin/blob/master/doc/access_control.md

### Anonymity
Similar to SQRL, allspan keys _should be made so they_ are pseudonymous, ensuring they are at most as traceable as bitcoin transactions.

## New terminology
- What [Camlistory said](https://github.com/camlistore/camlistore/blob/master/doc/terms.md) about blob, blogref, blob server, schema blob, claim, permanode, sync
- polis
- blocks
- exomemory
- Gestalt objects
- Oubliette access control (original phrase?)
- Event bubbles
- event horizon
- ASAP sharing
- trustring
- ring of fetchers
- datascapes
- goodwills
- trust route
- your routes

### Preexisting computer science jargon
- anonymity set
- metadata
- keyring
- download contract
- gossiping (protocol)
- plural backup solutions
- bound data
- content hash
- datahoarder
- datanaut
- FIDOnet
- remailer

