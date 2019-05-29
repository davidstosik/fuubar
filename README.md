Fuubar
================================================================================
[![Gem Version](https://img.shields.io/gem/v/fuubar.svg)](https://rubygems.org/gems/fuubar) ![Rubygems Rank Overall](https://img.shields.io/gem/rt/fuubar.svg) ![Rubygems Rank Daily](https://img.shields.io/gem/rd/fuubar.svg) ![Rubygems Downloads](https://img.shields.io/gem/dv/fuubar/stable.svg) [![Build Status](https://img.shields.io/travis/thekompanee/fuubar/master.svg)](http://travis-ci.org/thekompanee/fuubar) [![Code Climate](https://codeclimate.com/github/thekompanee/fuubar.svg)](https://codeclimate.com/github/thekompanee/fuubar)

fuubar is an instafailing [RSpec][rspec] formatter that uses
a progress bar instead of a string of letters and dots as feedback.

![examples][example-gif]

Installation
--------------------------------------------------------------------------------

```ruby
gem install fuubar

# or in your Gemfile

gem 'fuubar'
```

Usage
--------------------------------------------------------------------------------

In order to use fuubar, you have three options.

### Option 1: Invoke It Manually Via The Command Line ###

```
rspec --format Fuubar --color
```

### Option 2: Add It To Your Local `.rspec` File ###

```
# .rspec

--format Fuubar
--color
```

### Option 3: Add It To Your `spec_helper.rb` ###

```ruby
# spec/spec_helper.rb

RSpec.configure do |config|
  config.add_formatter 'Fuubar'
end
```

Advanced Usage
--------------------------------

### Customizing The Bar ###

fuubar exposes an RSpec configuration variable called
`fuubar_progress_bar_options` which, when set will be passed directly to
[ruby-progressbar][rpb-github] which does all the heavy lifting.  Take a look at
the [ruby-progressbar documentation][rpb-docs] for details on all of the options
you can pass in.

#### Example ####

Let's say for example that you would like to change the format of the bar. You
would do that like so:

```ruby
# spec/spec_helper.rb

RSpec.configure do |config|
  config.fuubar_progress_bar_options = { :format => 'My Fuubar! <%B> %p%% %a' }
end
```

would make it so that, when fuubar is output, it would look something like:

    My Fuubar! <================================                  > 53.44% 00:12:31

### Disabling Auto-Refresh ###

By default fuubar will automatically refresh the bar (and therefore the ETA)
every second.  Unfortunately this doesn't play well with things like debuggers.
When you're debugging, having a bar show up every second is undesireable.
[Pry][pry] gives us hooks so that we can automatically disable the refresh when
it's used. Unfortunately [byebug][byebug] does not and disabling the bar must be
done manually like so:

```ruby
# spec/spec_helper.rb

RSpec.configure do |config|
  config.fuubar_auto_refresh = false
end
```

Security
--------------------------------------------------------------------------------

fuubar is cryptographically signed. To be sure the gem you install hasn’t been
tampered with, follow these steps:

1. Add my public key (if you haven’t already) as a trusted certificate

```
gem cert --add <(curl -Ls https://raw.github.com/thekompanee/fuubar/master/certs/thekompanee.pem)
```

2. Install fuubar telling it to use security checks when possible.

```
gem install fuubar -P MediumSecurity
```

> **Note:** The `MediumSecurity` trust profile will verify signed gems, but
> allow the installation of unsigned dependencies.
>
> This is necessary because fuubar has a dependency on RSpec which isn't signed,
> and therefore we cannot use `HighSecurity`, which requires signed gems.

Credits
--------------------------------------------------------------------------------

fuubar was written by [Jeff Felchner][jefff-profile] and [Jeff
Kreeftmeijer][jeffk-profile]

![The Kompanee][kompanee-logo]

fuubar is maintained and funded by [The Kompanee, Ltd.][kompanee-site]

The names and logos for The Kompanee are trademarks of The Kompanee, Ltd.

License
--------------------------------------------------------------------------------

fuubar is Copyright &copy; 2010-2019 Jeff Kreeftmeijer and Jeff Felchner. It is
free software, and may be redistributed under the terms specified in the
[LICENSE][license] file.

[byebug]:        https://github.com/deivid-rodriguez/byebug
[example-gif]:   https://kompanee-public-assets.s3.amazonaws.com/readmes/fuubar-examples.gif
[jefff-profile]: https://github.com/jfelchner
[jeffk-profile]: https://github.com/jeffkreeftmeijer
[kompanee-logo]: https://kompanee-public-assets.s3.amazonaws.com/readmes/kompanee-horizontal-black.png
[kompanee-site]: http://www.thekompanee.com
[license]:       https://github.com/thekompanee/fuubar/blob/master/LICENSE.txt
[pry]:           https://github.com/pry/pry
[rpb-docs]:      https://github.com/jfelchner/ruby-progressbar/wiki/Options
[rpb-github]:    https://github.com/jfelchner/ruby-progressbar
[rspec]:         https://github.com/rspec
