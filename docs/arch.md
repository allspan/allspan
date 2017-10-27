
## Module diagram
TODO

## Design assumptions
The opposite of [Camlistore's assumptions](https://github.com/camlistore/camlistore/blob/master/doc/overview.txt), slightly tweaked:
* diskspace is limited
* bandwidth is metered
* CPU feels too slow
* people can't safely store private keys
* battery juice is precious

## Differences to related solutions
* https://github.com/camlistore/camlistore/blob/master/doc/arch.md is a server or service-based storage solution to last a lifetime, with considerations for not complicating future data arhealogy. Do read it's full [raison d'ètre](https://github.com/camlistore/camlistore/blob/master/doc/overview.md)
* [Upspin](http://upspin.io) is a global naming solution for files and users, meant to be usable across online services and walled garden social platforms.

## Useful technologies
- signed, traceable chain of claims, built like https://help.github.com/articles/signing-commits-with-gpg/
- SQRL for Gestalt keys, and possibly to help people store private keys

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

