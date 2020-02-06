# CHANGE LOG

## 2.1.0 (2020-01-14)

* [View the commits.](https://github.com/tedconf/fessonia/compare/2.0.0...2.1.0)
* [View the docs.](https://tedconf.github.io/fessonia/fessonia/2.1.0/)

## Bug Fixes

This release alters the way filter pad names are handled by the library.

* `FilterChain` output pad names are only applied in the command output (`cmd.toString()` and `cmd.toCommand()`) when `streamSpecifier()` is called on the `FilterChain` object. This fixes bug #24 (explicit output pad names added to commands where streams were not explicitly mapped, breaking resulting the `ffmpeg` command).

## Internal Changes

* The library now applies predictable names to output pads of `FilterChain` objects, replacing the previously used salted hash with a structure that provides for replication of output when running the same code multiple times.
* The `FilterNode` class has been altered to remove live `ffmpeg`-based validation and information retrieval for filters and their arguments, relying on `ffmpeg` to error when filters and arguments are not correct. This decision was made because the complexity in code and automated testing added by this validation were considered to be far greater than the protection provided by such validation.

## Documentation Changes

* A section has been added to the *About Fessonia* guide explaining how stream specifiers are used and what to expect when using explicit mappings.

## 2.0.0 (2019-12-03)

* [View the commits.](https://github.com/tedconf/fessonia/compare/1.0.1...2.0.0)
* [View the docs.](https://tedconf.github.io/fessonia/fessonia/2.0.0/)

## Breaking Changes

This release alters the way run log and progress log output from ffmpeg is handled by the library:

* The library now modifies the specified ffmpeg command by default, adding the `-progress` global option for use in eventing on progress updates. To disable this, you can pass `false` to the `spawn` method of `FFmpegCommand`.
* Run log returned by `FFmpegCommand` no longer includes progress lines, as those are treated as ephemeral and only used to generate the events.
* The `FFmpegCommand` no longer emits `failure` events, instead emitting `error` events with appropriate information on any `ffmpeg` failure with a new `FFmpegError` object.

### Documentation Changes

Documentation has been updated to reflect the new progress and log handling.

## 1.0.1 (2019-11-06)

* [View the commits.](https://github.com/tedconf/fessonia/compare/1.0.0...1.0.1)
* [View the docs.](https://tedconf.github.io/fessonia/fessonia/1.0.1/)

### New Features

This release adds support for appending and prepending `FilterNode`s to existing `FilterChain`s.

### Documentation Changes

* New documentation for 
* Fix of broken link ([@iameli](https://github.com/iameli)) [d8d5332](https://github.com/tedconf/fessonia/commit/d8d5332603ba0c95fa243ac1dd770126dd75512c)

### CI Changes

* Add explicit testing of node 12 [5ae9ce2](https://github.com/tedconf/fessonia/commit/5ae9ce2cceb38774d57b18c8135afb6faf6cda38)

## 1.0.0 (2019-10-04)

* [View the commits.](https://github.com/tedconf/fessonia/commits/e9c0b425321c172f0a5f56346985f34a827138d0)
* [View the docs.](https://tedconf.github.io/fessonia/fessonia/1.0.0/)

### New Features

This initial version provides an implementation of the core features:

* `FFmpegCommand` supporting `execute` and `spawn` and integrating a `FilterGraph` as part of the command
* `FFmpegInput` and `FFmpegOutput` supporting the various options supported by `ffmpeg`
* `FilterNode` and `FilterChain` supporting creation of filter chains for addition to the command's filter graph
* Stream selection and stream mapping from `FFmpegInput`s to `FilterChain`s and `FFmpegOutput`s, and from `FilterChain`s to `FFmpegOutput`s.

### Documentation Changes

Documentation auto-generation capability, as well as several tutorials and informational documents were created and published with this release. Documentation for this release can be found at [https://tedconf.github.io/fessonia/fessonia/1.0.0/](https://tedconf.github.io/fessonia/fessonia/1.0.0/).