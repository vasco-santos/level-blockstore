# level-blockstore

> Blockstore implementation with a level backend for content addressable data in ipfs-car. It follows the `ipfs-car` Blockstore Interface.

## Description

While packing files into [Content Addressable aRchives (CAR)](https://github.com/ipld/specs/blob/master/block-layer/content-addressable-archives.md), `ipfs-car` imports the given files into [unix-fs](https://github.com/ipfs/specs/blob/master/UNIXFS.md#importing). All the `unix-fs` graph needs to be computed, in order to get the root CID to create the resulting CAR file. This blockstore can be used to store the generated `unix-fs` temporarily, so that we can iterate them afterwards and create large CAR files.

This backend datastore can be used in `Node.js`, `Electron` and `Browser` environments.

## Install

```sh
# install it as a dependency
$ npm i level-blockstore
```

## Usage with ipfs-car

```js
import { pack } from 'ipfs-car/pack'
import { LevelBlockStore } from 'ipfs-car/blockstore/memory'

const { root, out } = await pack({
  input: [new Uint8Array([21, 31, 41])],
  blockstore: new LevelBlockStore()
})

const carParts = []
for await (const part of out) {
  carParts.push(part)
}
```
