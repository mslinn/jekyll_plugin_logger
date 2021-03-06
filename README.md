`jekyll_plugin_logger`
[![Gem Version](https://badge.fury.io/rb/jekyll_plugin_logger.svg)](https://badge.fury.io/rb/jekyll_plugin_logger)
===========

`jekyll_plugin_logger` is a Jekyll plugin, packaged as a Ruby gem, that provides colored console logs for Jekyll plugins.


## Usage

It looks within `_config.yml` for a key corresponding to the plugin progname.
For example, if the plugin's class is called `"MyPlugin"` then an entry called `plugin_loggers.MyPlugin`
will be read from the config file, if present.
If the entry exists, its value overrides the value specified when created.
If no such entry is found then the `log_level` value passed to `new` is used.

Below is a high-level example of how to create and use this plugin.
`site.config` is retrieved from `PluginMetaLogger.instance.config`;
for some plugins, that information is provided as a `site` parameter.
In that circumstance, `site.config` is a less verbose method of obtaining the same information.

```ruby
require "jekyll_plugin_logger"

module MyPlugin1
  @logger = PluginMetaLogger.instance.new_logger(self, PluginMetaLogger.instance.config)

  def my_plugin_method(text, query)
    @logger.debug { "text='#{text}' query='#{query}'" }
    # TODO write the rest of the method
  end

  # TODO write the rest of the plugin
end

PluginMetaLogger.instance.info { "Loaded my_plugin_1 v0.1.0 plugin." }
# Register MyPlugin1 here
```

By default, the above causes output to appear on the console like this:

```
INFO PluginMetaLogger: Loaded my_plugin_1 v0.1.0 plugin.
DEBUG MyPlugin1:  text='Hello world' query='Bogus query'
```

For more information about the logging feature in the Ruby standard library,
see https://ruby-doc.org/stdlib-2.7.2/libdoc/logger/rdoc/Logger.html



## Installation

Add this line to your Jekyll website's `_config.yml`:

```ruby
group :jekyll_plugins do
  gem 'jekyll_plugin_logger'
end
```

Install all of the dependent gems of your Jekyll website by typing:

    $ bundle install

Or install just this one gem by typing:

    $ gem install jekyll_plugin_logger


## Additional Information
More information is available on Mike Slinn's web site about
[Jekyll plugins](https://www.mslinn.com/blog/index.html#Jekyll).


## Development

After checking out the repo, run `bin/setup` to install dependencies, including development dependencies.

You can also run `bin/console` for an interactive prompt that will allow you to experiment.

### Build and Install Locally
To build and install this gem onto your local machine, run:
```shell
$ rake install:local
```

The following also does the same thing:
```shell
$ bundle exec rake install
jekyll_plugin_logger 1.0.0 built to pkg/jekyll_plugin_logger-0.1.0.gem.
jekyll_plugin_logger (1.0.0) installed.
```

Examine the newly built gem:
```shell
$ gem info jekyll_plugin_logger

*** LOCAL GEMS ***

jekyll_plugin_logger (1.0.0)
    Author: Mike Slinn
    Homepage:
    https://github.com/mslinn/jekyll_plugin_logger
    License: MIT
    Installed at: /home/mslinn/.gems

    Generates Jekyll logger with colored output.
```

### Build and Push to RubyGems
To release a new version,
  1. Update the version number in `version.rb`.
  2. Commit all changes to git; if you don't the next step might fail with an unexplainable error message.
  3. Run the following:
     ```shell
     $ bundle exec rake release
     ```
     The above creates a git tag for the version, commits the created tag,
     and pushes the new `.gem` file to [RubyGems.org](https://rubygems.org).


## Contributing

1. Fork the project
2. Create a descriptively named feature branch
3. Add your feature
4. Submit a pull request


## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
