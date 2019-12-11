gogo-release is a simple POSIX shell script to:

1. Cross-compile binaries to various different targets.
2. Optionally compress the binaries.

It's the simpler and unix-beardy brother of [go-releaser][gor].

Configure it by adding a `.gogo-release` file or just by editing the source.

Usage:

1. *[Mad coding]*.
2. Hide yo wife, hide yo kids, commit yo code.
3. Create a new tag.
4. `gogo-release`
5. Create new GitHub release, upload contents of `dist`.
6. Have a celebratory beer, release party, drug binge, orgy, Satanic sacrifice.

Notes:

1. Cross-compiling code that uses cgo is tricky as cross-compiling C code is
   tricky:

   1. Make sure you have the required C compiler cross-build tools installed ;
      you can usually install these from your distro's package manger (names
      vary; searching for `cross` should work).
   2. Make sure `CGO_ENABLED=1` is set, e.g. by adding `export CGO_ENABLED=1` to
      `.gogo-release`.
   3. Make sure the right compiler is used by adding `CC=..` to the build
      matrix.

   Support is minimal at the moment; tools like [xgo][xgo] may offer a better
   experience if you want to cross-compile to many different platforms.

2. A previous version also included code for automatically creating a GitHub
   release and uploading it. I later removed this as I felt it was too complex
   and uploading is just a few clicks (I got carried away). You can still it in
   your own shell script if you want:
   https://github.com/arp242/gogo-release/blob/5a2de679869746331b63f942dd381334f50d3dd3/gogo-release#L70

[gor]: https://github.com/goreleaser/goreleaser
[xgo]: https://github.com/karalabe/xgo
[sqlite]: https://github.com/mattn/go-sqlite3/issues/384
