# MaLSAMi project documentation


Welcome to the MaLSAMi project documentation.

In here we will document our progress and almost all subprojects or programs
we will create or write.
If you want to take a deeper look in our open source code projects please refer to the [MaLSAMi Github Page](https://github.com/malsami)

## About the project

You can find a general description of the project MaLSAMi in the [About Section](/about)

## Prerequisite

To contribute to this documentation please download the source code from the [MaLSAMi Documentation Repository](https://github.com/malsami/documentation)
and follow the instructions at [MkDocs](http://www.mkdocs.org/#installation).

## Documentation structure

The documentation is structured into different subpages which are representing subprojects of the project MaLSAMi.
Nevertheless also analysis results or specifications of the projects can be described in a subpage.


## Commands

To work with MkDocs after installing it, you can use these commands

* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

To upload the documentation to the git repository please following command, but be aware that changes might be immediately visible.

* `mkdocs gh-deploy` - Uploads build documentation sites to gh-pages branch

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
