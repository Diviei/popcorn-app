# Unicorns!

This is a fork of [now abadoned][medium] Popcorn Time app. This is the *uni*fied place for community to work on it. I've reopened the [issues section][issues] so yes, we can get back to a normal development cycle.

### Todo list

* Binary builds
* Website (probably just fork [the original one][githubio])

[medium]:   https://medium.com/p/93f890b8c9f4
[issues]:   https://github.com/unicorn-time/popcorn-app/issues
[githubio]: https://github.com/popcorn-time/popcorn-time.github.io


# Popcorn Time [![Dependency Status](https://david-dm.org/unicorn-time/popcorn-app.png?theme=shields.io)](https://david-dm.org/unicorn-time/popcorn-app)

## Idea

To allow any computer user to watch movies easily streaming from torrents, without any particular knowledge.

![Demo Screenshot][screenshot]

[screenshot]: https://i.imgur.com/OLanAVR.png

### Status

Under development (RC1) for Mac OSX - Windows - Linux.
 
### APIs

**Currently used:**
- [YIFY][] movie torrents API.
- [OpenSubtitles][] for subtitles
- [TheMovieDB][] for movies metadata.

[YIFY]: http://yts.re/api
[OpenSubtitles]: http://trac.opensubtitles.org/projects/opensubtitles/wiki/XMLRPC
[TheMovieDB]: http://www.themoviedb.org/

## Building

### Dependencies

You will need nodejs and grunt:

    $ npm install -g grunt-cli

### Build

Install the node modules:

    $ npm install

Build with:

    $ grunt nodewkbuild

By default it will build for your current platform however you can control that
by specifying a comma separated list of platforms in the `platforms` option to
grunt:

    $ grunt nodewkbuild --platforms=linux32,linux64,mac,win

You can also build for all platforms with:

    $ grunt nodewkbuild --platforms=all

## Any problem?

### Regarding superagent dependency
Due to [wrong browser verification](https://github.com/visionmedia/superagent/issues/95) on a dependency, this hard fix must be applied.
Replace `node_modules/moviedb/node_modules/superagent/index.js` contents with:
```javascript
// if (typeof window != 'undefined') {
//   module.exports = require('./lib/superagent');
// } else if (process.env.SUPERAGENT_COV) {
//   module.exports = require('./lib-cov/node');
// } else {
  module.exports = require('./lib/node');
// }
```

### Regarding Video, MP4 H264 Playback
- Info: https://github.com/rogerwang/node-webkit/wiki/Support-mp3-and-h264-in-video-and-audio-tag
- Needed to build a custom build of node-webkit that adds h264 support (or you can download ready-to-go builds from https://file.ac/s4Lt3Vo6rls/)
- Alternatively, we can replace a .so and .dll file from the correspondent Chrome build to node-webkit and node-webkit.exe


## Development
- Run `compass watch` in Terminal for CSS compiling and listen to future changes.
- [How to build with SublimeText](https://github.com/rogerwang/node-webkit/wiki/Debugging-with-Sublime-Text-2-and-3)
- Currently Gaze to watch all files and reload the app is disabled due to memory leaks and unstability.
- Run node-webkit from the root directory with --debug to enable debugging mode like so ```node-webkit . --debug```
