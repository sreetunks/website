source "https://rubygems.org"
# Jekyll version to use
gem "jekyll", "~> 4.1.0"
# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "jekyll-theme-console"
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem 'wdm', '~> 0.1.1', :install_if => Gem.win_platform?

gem "webrick", "~> 1.8"
