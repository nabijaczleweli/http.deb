# http [![Travis build status](https://travis-ci.org/thecoshman/http.svg)](https://travis-ci.org/thecoshman/http) [![AppVeyor build status](https://ci.appveyor.com/api/projects/status/7knk9lnptn1njro5?svg=true)](https://ci.appveyor.com/project/thecoshman/http) [![Licence](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE) [![Crates.io version](https://img.shields.io/crates/v/https.svg)](https://crates.io/crates/https)
Host These Things Please - a basic HTTP server for hosting a folder fast and simply

## Selected features

See [the manpage](http.md) for full list.

  * [x] Symlinks followed by default (disableable via `-s` option)
  * [x] Index generation for directories
  * [x] Sane defaults (like hosted dir (`.`) and port (first free one from range `8000`-`9999`))
  * [x] Correct MIME type for served files
  * [x] Handled request methods: OPTIONS, GET, PUT, DELETE, HEAD and TRACE ("writing" methods are off by default, enable via `-w` switch)
  * [x] Proper handling of percent-encoded URLs (like `асдф fdsa`)
  * [x] Good symlink handling compatible with Windows
  * [x] Multitude of information in directory indices
  * [x] Serving index files like `index.{html,htm,shtml}` from directories (disableable via `-i` switch)
  * [x] Drag&Drop to upload files (with `-w` specified)
  * [x] Smart encoding of generated and filesystem-originating responses (disableable via `-e` switch)
  * [x] Full Range header support
  * [x] Hosting with an <sub>(optional)</sub> optionally autogenerated TLS certificate
  * [x] Arbitrarily nested username/password authentication
  * [x] Per-request bandwidth cap
  * [x] Per-extension-overridable MIME-types with reasonable guesses
  * [x] [WebDAV/RFC2518](https://tools.ietf.org/html/rfc2518) support, tested with the Linux [`davfs2`](http://savannah.nongnu.org/projects/davfs2) helper, Windows network filesystem support (out-of-box), and the Total Commander [WebDAV plugin](https://www.ghisler.com/plugins.htm)
  * [x] [RFSAPI](https://github.com/nabijaczleweli/rfsapi-rs) support ([format spec](https://rawcdn.githack.com/nabijaczleweli/rfsapi-rs/doc/rfsapi/index.html#format-spec)) (explorable from commandline with [D'Oh](https://github.com/thecoshman/doh))

## [Manpage](http.md)

## Installation

If you have `cargo` installed (you're a Rust developer) all you need to do is:

```sh
cargo install https
```

Which will install `http` and `httplz` (identical, disable one or another if they clash) in the folder where all other binaries go.

If, however, you're not a Rust developer, but you have `sh`-like shell, you can use an installer (works on Windows and Linux):

```sh
curl -SsL https://cdn.rawgit.com/thecoshman/http/master/install.sh | sh
# or, if you like taking precautions
sh -c "$(curl -SsL https://cdn.rawgit.com/thecoshman/http/master/install.sh)"
```

You can change the installation directory by setting the `PREFIX` environment variable (default - `/usr/bin`):

```sh
PREFIX=$HOME/bin curl -SsL https://cdn.rawgit.com/thecoshman/http/master/install.sh | sh
# Windows:
set PREFIX=D:\Akces
curl -SsL https://cdn.rawgit.com/thecoshman/http/master/install.sh | sh
```

If you're on a Debian-based amd64 machine, you can also grab a `.deb` package from the [latest release page](https://github.com/thecoshman/http/releases/latest).

If you're on Windows and prefer a more guided installation (or you don't have a shell),
you can download the Windows installer from the [latest release's page](https://github.com/thecoshman/http/releases/latest).
(Note: you can add /D *INSTALLDIR* to installer command line to change the installation directory.)

## Aims
The idea is to make a program that can compile down to a simple binary that can be used via Linux CLI to quickly take the current directory and serve it over HTTP. Everything should have sensible defaults such that you do not *have* to pass parameters like what port to use.

  * [x] Sub directories would be automatically hosted.
  * [ ] Symlinks will not be followed by default (in my opinion, this is more likely to be a problem than an intended thing).
  * [x] Root should not be required.
  * [x] If an index file isn't provided, one will be generated (in memory, no touching the disk, why would you do that you dirty freak you), that will list the current files and folders (and then sub directories will have index files generated as required)
  * [x] Changes made to files should be reflected instantly, as I don't see why anything would be cached... you request a file, a file will be looked for

It's not going to be a 'production ready' tool, it's a quick and dirty way of hosting a folder, so whilst I'll try to make it secure, it is not going to be a serious goal.
