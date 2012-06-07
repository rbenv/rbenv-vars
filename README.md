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

### Variable File

Define environment variables in an `.rbenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    RUBY_GC_MALLOC_LIMIT=50000000
    RUBY_HEAP_MIN_SLOTS=15000
    RUBY_FREE_MIN=4096

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `GEM_PATH`:

    GEM_PATH=$GEM_PATH:/u/shared/gems

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.rbenv/vars` file will be set
first. Then variables specified in `.rbenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.rbenv-vars` file in the current directory are set last.

Use the `rbenv vars` command to print all environment variables in the
order they'll be set.

### Alternate Variable File

It is a good idea to segregate sensitive information like passwords
and account infomation from your public code repository.

To help with this, an alternate file can be used with the filename 
`.rbenv-vars-<yourfile>`.  The alternate file will be loaded before 
the normal `.rbenv-vars` file.

For example, your application may require an environment variable with
a database connect string that contains a password.

Alternate file: `.rbenv-vars-passwords`

    DB_PASSWORD=mypassword

Normal file: `.rbenv-vars`

    DB_CONNECT_STRING=postgres://dbuser:${DB_PASSWORD}@localhost/my_database

In this situation, you would include `.rbenv-vars-passwords` in your .gitignore
file.

## License

&copy; 2011 Sam Stephenson. Released under the MIT license. See
`LICENSE` for details.
