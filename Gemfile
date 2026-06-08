# frozen_string_literal: true

source "https://rubygems.org"

ruby ">= 3.1"

# Load theme dependencies from gemspec
gemspec

# Standard gems required for Jekyll
gem "csv"
gem "logger"
gem "base64"

# Testing
group :test do
  gem "html-proofer", "~> 5.0"
end

# Jekyll plugins
group :jekyll_plugins do
  gem "jekyll-youtube"
end

# Windows and JRuby specific gems
install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 2.0"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.2.0", install_if: Gem.win_platform?
