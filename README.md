# Intro

We are frequently packaging all gems in the gem-list on our jenkins instance.
Results end up on  http://pulp.inuits.eu/pulp/repos/rubygems/




Package are build on CentOS Boxen.


# Parameters

You can modify certain parameters by exporting these environment variables before running the script:

* `GEM_PREFIX`

    Translates into fpm's `--gem-prefix` argument.<br/>
    Defaults to `/usr/lib/ruby/gems/1.8`.

* `GEM_BIN_PATH`

    Translates into fpm's `--gem-bin-path` argument.<br/>
    Defaults to `/usr/bin`.

* `TARGET`

    File containing list of gems to build. You can also override this by providing the filename as an argument to the script.<br/>
    Defaults to `gem-list`.


## Examples:

### Change the gem prefix.

    export GEM_PREFIX=/usr/local/lib/ruby/gems/1.8
    ./build-gems

### Choose a custom file with gems.

    ./build-gems minimal

    # This is the same as
    export TARGET=minimal
    ./build-gems

# Gem list file format

Each line is formatted in the following way:

`<gem name>:[version]:[extra fpm options]`

* `<gem name>`: is a required option (&lt;/captain obvious&gt;).
* `[version]`: optional specific version to build. Defaults to the latest 'stable' release if not specified.
* `[extra fpm options]`: Can be used to specify dependencies manually.

Lines starting with `#` are ignored.

## Example file:

    sqlite3::--provides "rubygem(sqlite3-ruby)" --depends "sqlite >= 3.6.16"
    backports
    backports:2.3.0
    puppet-lint:pre

