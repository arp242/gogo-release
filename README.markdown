gogo-release is a simple POSIX shell script to:

1. Cross-compile binaries to various different targets.
2. Optionally compress the binaries.

It's the simpler and unix-beardy brother of [go-releaser][gor].

Configure it by just editing the source or adding a `.gogo-release` file; this
is simply a shell script that's sourced and can be used to set/override some
variables. [Here is an example][ex]. See the `gogo-release` script for a list of
things you can set with documentation.

Usage:

1. *[Mad coding]*.
2. Hide yo wife, hide yo kids, commit yo code.
3. Create a new tag.
4. `gogo-release`
5. Create new GitHub release, upload contents of `dist`.
6. Have a celebratory beer, release party, drug binge, orgy, Satanic sacrifice.

Notes:

1. The current commit must have a tag, so if you want to build v1.2.0:

       $ git checkout v1.2.0
       $ gogo-release

   You can also add a version as a commandline argument; this will only put the
   version in the name, and *won't* check out the git commit:

       $ gogo-release v1.2.0

   This is mostly intended for testing.

2. Cross-compiling code that uses cgo is tricky as cross-compiling C code is
   tricky; I wrote a bit more about that over here: [Statically compiling Go
   programs][static]. In brief:

   1. Make sure you have the required C compiler cross-build tools installed;
      you can usually install these from your distro's package manger (names
      vary; searching for `-linux-` should work).
   2. Make sure `CGO_ENABLED=1` is set, e.g. by adding `export CGO_ENABLED=1` to
      `.gogo-release`.
   3. Make sure the right compiler is used by adding `CC=..` to the build
      matrix.
   4. You probably want to add `-ldflags='-extldflags=-static'` to create
      statically linked binaries. Otherwise, make sure to use an older libc
      version for best compatability.

   An alternative might be [xgo][xgo], which may be a bit easier to
   cross-compile cgo code depending on what you want and personal preferences.

3. Define a `gogo_before_exit` function in your `.gogo-release` to run something
   after everything is done. Just add the lines to the script if you want to run
   something before the building starts; for example:

       start=$(date +%s)
       gogo_before_exit() {
           echo "Took $(( $(date +%s) - $start )) seconds"
           ls -lh "$tmp" | awk '{print $5 " " $9}'
       }

4. A previous version also included code for automatically creating a GitHub
   release and uploading it. I later removed this as I felt it was a bit too
   complex and *automagic*. Uploading is just a few clicks anyway, so it doesn't
   really save that much effort (I got carried away). [You can still add it in
   `gogo_before_exit` if you want][gh].


[ex]: https://github.com/zgoat/goatcounter/blob/master/.gogo-release
[gh]: https://github.com/arp242/gogo-release/blob/5a2de679869746331b63f942dd381334f50d3dd3/gogo-release#L70
[gor]: https://github.com/goreleaser/goreleaser
[xgo]: https://github.com/karalabe/xgo
[sqlite]: https://github.com/mattn/go-sqlite3/issues/384
[static]: http://arp242.net/static-go.html
