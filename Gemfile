# frozen_string_literal: true

source "https://rubygems.org"

gemspec

gem "html-proofer", "~> 5.0", group: :test

platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]



# # frozen_string_literal: true

# source "https://rubygems.org"

# gemspec


# group :test do
#   gem "html-proofer", "~> 5.0.9"
# #  gem "html-proofer", "~> 4.4.3"
# end

# gem 'jekyll-analytics'

group :jekyll_plugins do
    gem "jekyll-youtube"
end

# # Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# # and associated library.
# install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
#   gem "tzinfo", "~> 2.0.6"
#   gem "tzinfo-data"
# end

# # Performance-booster for watching directories on Windows
# gem "wdm", "~> 0.2.0", :install_if => Gem.win_platform?
