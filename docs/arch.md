
## Module diagram
TODO

## Design assumptions

### Not like Camlistore
The opposite of [Camlistore's assumptions](https://github.com/camlistore/camlistore/blob/master/doc/overview.txt) while still agreeing with [Camlistore's principles](https://github.com/camlistore/camlistore/blob/master/doc/principles.md):
* diskspace is limited _in practice_
* bandwidth is metered
* CPU feels too slow
* people can't safely store private keys

### Additional assumtions
* battery juice is precious
* someone is watching and storing all connection metadata on internet and other public networks
* democracy and freedom maybe won't last
* unfiying filesystems and naming is hard

## Goals

## Differences to related _open_ solutions
* [Camlistore's design](https://github.com/camlistore/camlistore/blob/master/doc/arch.md) gives you a server or service-based storage solution to last a lifetime, with considerations for not complicating future data arhealogy. Do read it's full [raison d'ètre](https://github.com/camlistore/camlistore/blob/master/doc/overview.md)
* [Upspin](http://upspin.io) is a global naming solution for files and users, meant to be usable across online services and walled garden social platforms.
* [Hashbackup](http://www.hashbackup.com/home/features) is Dropbox minus the sharing, and likely feature completed.
* (Diaspora*)[https://wiki.diasporafoundation.org/Architecture_overview] is a good data transport, but routing is federated. Profile, sharing etc was _initially_ designed very close to something Allspan could be built on top of. It ticks many boxes, but requires trusted system operators.

## Useful technologies
- signed, traceable chain of claims, built like https://help.github.com/articles/signing-commits-with-gpg/
- [SQRL](https://www.grc.com/sqrl/sqrl.htm) for Gestalt keys, and possibly to help people store private keys
- [Snappy compression](https://google.github.io/snappy/) for cpu-friendly space/&time saving
- private long-term routing by [paid remailers](http://nakamotoinstitute.org/for-pay-remailers/)

## Prior art in a wide sense
- What's at https://github.com/camlistore/camlistore/blob/master/doc/prior-art.md
- All mentions under [Diff. to realted solutions](https://github.com/allspan/allspan/blob/master/docs/arch.md#differences-to-related-open-solutions)
- File sync and dropbox services
- [Android Syncbase](https://vanadium.github.io/syncbase/) is offline-first P2P backup.
- storing and sharing solutions; FreeNet, Gnutella, Napster, BitTorrent, tor, i2p, IPFS, Storj, Sia
- social networks, and Diaspora*, Identi.ca, Voat, etc

## Important processes (protocol)
- finding routes
- offering blobs
- sharing metadata
- fetching a file

## Security
- Use only battle hardened crypto and in the same way as it's used elsewhere by bigger targets. Compare Bitcoin SHA256 and EC.

### Access control
Compare https://github.com/upspin/upspin/blob/master/doc/security.md and https://github.com/upspin/upspin/blob/master/doc/access_control.md

### Anonymity


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

