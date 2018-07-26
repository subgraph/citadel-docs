Citadel Documentation
=====================

## Contributing

There are three ways to contribute to this documentation

**Documentation**

The docs in this repo are simple `markdown` files. To create new entries, edit
existing docs, or fix typos you can simply use Github's in-browser editing

- [Source Files](https://github.com/subgraph/citadel-docs/tree/master/markdown)

**HTML Preview**

Similarly, you can make changes to the source files in the `markdown` folder 
and then build the HTML output by installing the following:

- [Rust](https://rustup.rs)
- [mdBook](https://github.com/rust-lang-nursery/mdBook)

To view an up-to-date build of the documenation, run the following command, 
which will open it in your default web browser.

```
mdbook build --open
```

Or you can view (and reload live changes) via an HTTP server

```
mdbook serve
```

While viewing live updated docs at [http://localhost:3000](http://localhost:3000)

**Gnome Application**

To run `Citadel Docs` as a standalone Gnome application, you need to install 
the following dependencies (on a Debian system):

```
sudo apt-get install libwebkit2gtk-4.0-dev libwebkit2-sharp-4.0-cil libwebkit2-sharp-4.0-cil-dev
```

Then build the up-to-date documentation as well as the Gnome application with:

```
mdbook build
./autogen.sh --prefix=/home/user/.local
```

Then install the application with the following:

``
make install
```

- Installs the application in `/home/user/.local/bin`
- Installs the `citadel-docs.desktop` file in `/home/user/.local/share/applications`

The application should be viewable in the `Show Applications` grid of apps
