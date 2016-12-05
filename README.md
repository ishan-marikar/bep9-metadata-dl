# bep9-metadata-dl

### Download the metadata from peers using infohash only

This module uses [bittorrent-protocol](https://github.com/feross/bittorrent-protocol), [ut_metadata](https://github.com/feross/ut_metadata) and
[torrent-discovery](https://github.com/feross/torrent-discovery) modules of [WebTorrent](https://github.com/feross/webtorrent) to download the info-dictionary part of a .torrent file using infohash of magnet links only.

## features

- simple API
- find peers from the DHT network
- support callbacks and Promise

## install

```
npm install
```

## API

### `fetchMetadata(infohash, [opts], [callbackFn])`
### `fetchMetadata.fromPeer(infohash, peerAddress, [opts], [callbackFn])`

### Example:
```js
const fetchMetadata = require('bep9-metadata-dl');

// infohash of ubuntu-16.04.1-server-amd64.iso
const INFO_HASH = '90289fd34dfc1cf8f316a268add8354c85334458'; 

fetchMetadata(INFO_HASH, { maxConns: 10, fetchTimeout: 30000, socketTimeout: 5000 },
  (err, metadata) => {
  if (err) {
    console.log(err);
    return;
  }
  console.log(`[Callback] ${metadata.name.toString('utf-8')}`);
});
```
### Or Promise based:
```js
const fetchMetadata = require('bep9-metadata-dl');

// infohash of ubuntu-16.04.1-server-amd64.iso
const INFO_HASH = '90289fd34dfc1cf8f316a268add8354c85334458'; 

fetchMetadata(INFO_HASH, { maxConns: 10, fetchTimeout: 30000, socketTimeout: 5000 })
.then(metadata => {
  console.log(`[Promise] ${metadata.name.toString('utf-8')}`);
}).catch(err => {
  console.log(err);
});
```
### Download directly from a peer:
```js
const fetchMetadata = require('bep9-metadata-dl');

// infohash of ubuntu-16.04.1-server-amd64.iso
const INFO_HASH = '90289fd34dfc1cf8f316a268add8354c85334458'; 

fetchMetadata.fromPeer(INFO_HASH, '88.166.72.111:5', { timeout: 5000 }, 
  (err, metadata) => {
  if (err) {
    console.log(err);
    return;
  }
  console.log(`[Callback] ${metadata.name.toString('utf-8')}`);
});
```
### Download directly from a peer, Promise based:
```js
const fetchMetadata = require('bep9-metadata-dl');

// infohash of ubuntu-16.04.1-server-amd64.iso
const INFO_HASH = '90289fd34dfc1cf8f316a268add8354c85334458'; 

fetchMetadata.fromPeer(INFO_HASH, '88.166.72.111:5', { timeout: 5000 })
.then(metadata => {
  console.log(`[Promise] ${metadata.name.toString('utf-8')}`);
}).catch(err => {
  console.log(err);
});
```

## License

MIT. Copyright (c) [Hong Yan](https://github.com/homeryan).
