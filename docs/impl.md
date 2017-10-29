# Implementation details

## Fetch a file
Ideally, to avoid latency and transfer window buildup, fetching a file should be done via HTTP/2 or QUIC, whichever had the instant SSL connection without handshake.
The request should include enough info so that the server can send all needed objects/blobs without additional requests.
That makes the request far cleaner than https://github.com/upspin/upspin/blob/master/doc/images/arch/readfile.png while still not necessarily leaking any additional data.

HTTP/2 etc might allow prioritization, so maybe folder structures, metadata, the first + maybe last blobs of bigger files, or file-sequential streaming so a client can show media files wihtout assembling the file first on disk.

## Create a new share (on published data)
The metadata and share key can simply be transfered to the recipient as a JWT object.
