# fsevents [![NPM](https://nodei.co/npm/fsevents.png)](https://nodei.co/npm/fsevents/)

Native access to MacOS FSEvents in [Node.js](https://nodejs.org/)

The FSEvents API in MacOS allows applications to register for notifications of
changes to a given directory tree. It is a very fast and lightweight alternative
to kqueue.

This is a low-level library. For a cross-platform file watching module that
uses fsevents, check out [Chokidar](https://github.com/paulmillr/chokidar).

## Installation

```sh
npm install fsevents
```

## Usage

```js
const fsevents = require('fsevents');
const stop = fsevents.watch(__dirname, (path, flags, id) => {
  const info = fsevents.getInfo(path, flags, id);
}); // To start observation
stop(); // To end observation
```

The callback passed as the second parameter to `.watch` get's called whenever the operating system detects a
a change in the file system. It takes three arguments:

`(path, flags, id) => {}`

 * `path` - which is a string naming the path of the item in the filesystem that changed
 * `flags` - a numeric value describing what the change was
 * `id` - a unique-id identifying this specific event

###### `fsevents.getInfo(path, flags, id): FsEventInfo => {}`

The `getInfo` function takes the `path`, `flags` and `id` arguments and converts those parameters into a structure
that is easier to digest to determine what the change was.

The `FsEventInfo` has the following shape:

```js
{
  "event": "<created|modified|deleted|moved|root-changed|unknown>",
  "path": "<path-that-this-is-about>",
  "type": "<file|directory|symlink>",
  "changes": {
    "inode": true,   // Had iNode Meta-Information changed
    "finder": false, // Had Finder Meta-Data changed
    "access": false, // Had access permissions changed
    "xattrs": false  // Had xAttributes changed
  },
  "flags": <raw-flags>
}
```

## License

The MIT License Copyright (C) 2010-2018 by Philipp Dunkel, Ben Noordhuis, Elan Shankar — see LICENSE file.

Visit our [GitHub page](https://github.com/fsevents/fsevents) and [NPM Page](https://npmjs.org/package/fsevents)
