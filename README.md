# rbenv-vars

This is a plugin for [rbenv](https://github.com/sstephenson/rbenv)
that lets you set global and project-specific environment variables
before spawning Ruby processes.

## Installation

To install rbenv-vars, clone this repository into your
`~/.rbenv/plugins` directory. (You'll need a recent version of rbenv
that supports plugin bundles.)

    $ mkdir -p ~/.rbenv/plugins
    $ cd ~/.rbenv/plugins
    $ git clone https://github.com/sstephenson/rbenv-vars.git

## Usage

Define environment variables in an `.rbenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    RUBY_GC_MALLOC_LIMIT=50000000
    RUBY_HEAP_MIN_SLOTS=15000
    RUBY_FREE_MIN=4096

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `GEM_PATH`:

    GEM_PATH=$GEM_PATH:/u/shared/gems

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

    JAVA_OPTS?=-server -Xmx768m -Xms768m -Xmn128m -Xss20m

In the above case, `JAVA_OPTS` will only be set if `$JAVA_OPTS` is
currently empty (i.e., if `[ -z "$JAVA_OPTS" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.rbenv/vars` file will be set
first. Then variables specified in `.rbenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.rbenv-vars` file in the current directory are set last.

Use the `rbenv vars` command to print all environment variables in the
order they'll be set.

## Version History

**1.1.0** (June 25, 2012)

* Added support for conditional variable assignments using
  `?=`. Thanks to Scott Gonyea for the patch.

**1.0.0** (September 27, 2011)

* Initial public release.

## License

&copy; 2012 Sam Stephenson. Released under the MIT license. See
`LICENSE` for details.
