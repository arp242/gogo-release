gogo-release is a simple shell script to:

1. Create a new Git tag (or re-use existing tag pointing to the current commit).
2. Cross-compile binaries to various different targets.
3. Compress the binaries.
4. If GITHUB_TOKEN is set, create a GitHub release and upload the compressed
   binaries to GitHub. Get a token at https://github.com/settings/tokens
   (Settings → Developer settings → Personal access tokens) with `repo` scope.

It's the simpler and unix-beardy brother of [go-releaser][gor].

Configure it by editing the source; it shouldn't be hard to add support for
mercurial or GitLab. Please let me know if yo do.

Usage:

1. *[Mad coding]*.
2. Hide yo wife, hide yo kids, commit yo code.
3. ` export GITHUB_TOKEN=..`
4. `gogo-release <tagname>`
5. Have a celebratory beer, release party, drug binge, orgy, Satanic sacrifice.

[gor]: https://github.com/goreleaser/goreleaser
