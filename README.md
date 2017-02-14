[![Build Status](https://travis-ci.org/othiym23/packard-read-metadata.svg)](https://travis-ci.org/othiym23/packard-read-metadata)
[![Coverage Status](https://coveralls.io/repos/othiym23/packard-read-metadata/badge.svg?branch=master)](https://coveralls.io/r/othiym23/packard-read-metadata?branch=master)

# @packard/read-metadata

Given a path and, optionally, a
[`stats`](https://nodejs.org/api/fs.html#fs_class_fs_stats) object, produce a
[`@packard/model`](https://www.npmjs.com/package/@packard/model)
[Track](https://www.npmjs.com/package/@packard/model#track) populated with all
of the metadata from that track.

Can read metadata from `.mp3` MPEG-2 Layer III files with embedded ID3 and
ID3v2 tags, `.flac` FLAC files with Ogg Vorbis comments, and `.m4a` AAC files
embedded in QuickTime containers using iTunes QuickTime atoms. Does some
twisted things in its test code to ensure that the tests are meaningful.

## usage

```js
var scan = require('@packard/read-metadata').scan
scan({ path: empty, stats: stats }, progressGroups)
  .then(function (track) {
    console.log('track:', track)
  })
```

## API

### require('@packard/read-metadata').scan(info, progressGroups)

#### `info` fields

- `path`: String path to file to scan. Required.
- `stats`: Standard `Stats` associated with the audio file for the track. Will
  be populated if not included.
- `streamData`: Object literal containing metadata previously pulled from file.
  Defaults to `{}`.
- `tags`: Object literal containing metadata for the audio contained in the
  file. Defaults to `{}`.
- `musicbrainzTags`: Object literal containing MusicBrainz metadata associated
  with the audio contained in the file. Defaults to `{}`.

## external dependencies

To run its tests, `@packard/read-metadata` uses eyeD3 to write tags to MP3
files, `metaflac` (from the same distribution as `flac`) to set FLAC tags, and
[Atomic Parsley](https://github.com/wez/atomicparsley) to write tags to M4A
files.
