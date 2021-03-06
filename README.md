# rspec-boilerplate-config

Boilerplate configuration for RSpec, including support files for Devise, FactoryBot, and Pundit, which are all popular and widely used Ruby on Rails tools. I've also included common controller macros and a database cleaner.

My configurations use the following gems as dependencies: 

```
# note that capybara is included by default in Rails 5.1+
gem 'capybara'

gem 'database_cleaner-active_record'
gem 'factory_bot_rails'
gem 'faker', git: 'https://github.com/faker-ruby/faker.git', branch: 'master'
gem 'pundit-matchers', '~> 1.6.0'
gem 'rspec-rails', '~> 4.0.2'
gem 'rubocop-rspec', require: false
gem 'simplecov', require: false
gem 'webmock'
```

I made this because I've spent way too much time in the past configuring RSpec from zero. This repository can be cloned, and the `support` path moved to the `spec` app directory, or used referentially. If cloned, please ensure that `rails_helper.rb` contains the following (the repo also has sample helpers for both `rails` and `spec`):

```
# This file is copied to spec/ when you run 'rails generate rspec:install'
require 'spec_helper'
ENV['RAILS_ENV'] ||= 'test'
require File.expand_path('../config/environment', __dir__)
# Prevent database truncation if the environment is production
abort('The Rails environment is running in production mode!') if Rails.env.production?
require 'rspec/rails'

# Add additional requires below this line. Rails is not loaded until this point!
require 'devise'
require 'support/factory_bot'
require 'simplecov'
require 'capybara/rails'
require 'support/database_cleaner'
require 'support/devise'
require 'support/pundit_matcher'
require 'webmock/rspec'

SimpleCov.start

# Requires supporting ruby files with custom matchers and macros, etc, in
# spec/support/ and its subdirectories. Files matching `spec/**/*_spec.rb` are
# run as spec files by default. This means that files in spec/support that end
# in _spec.rb will both be required and run as specs, causing the specs to be
# run twice. It is recommended that you do not name files matching this glob to
# end with _spec.rb. You can configure this pattern with the --pattern
# option on the command line or in ~/.rspec, .rspec or `.rspec-local`.
#
# The following line is provided for convenience purposes. It has the downside
# of increasing the boot-up time by auto-requiring all files in the support
# directory. Alternatively, in the individual `*_spec.rb` files, manually
# require only the support files necessary.
#
# Dir[Rails.root.join('spec', 'support', '**', '*.rb')].sort.each { |f| require f }

# Checks for pending migrations and applies them before tests are run.
# If you are not using ActiveRecord, you can remove these lines.
begin
  ActiveRecord::Migration.maintain_test_schema!
rescue ActiveRecord::PendingMigrationError => e
  puts e.to_s.strip
  exit 1
end
RSpec.configure do |config|
  # Remove this line if you're not using ActiveRecord or ActiveRecord fixtures
  config.fixture_path = "#{::Rails.root}/spec/fixtures"

  # If you're not using ActiveRecord, or you'd prefer not to run each of your
  # examples within a transaction, remove the following line or assign false
  # instead of true.
  config.use_transactional_fixtures = true

  # You can uncomment this line to turn off ActiveRecord support entirely.
  # config.use_active_record = false

  # RSpec Rails can automatically mix in different behaviours to your tests
  # based on their file location, for example enabling you to call `get` and
  # `post` in specs under `spec/controllers`.
  #
  # You can disable this behaviour by removing the line below, and instead
  # explicitly tag your specs with their type, e.g.:
  #
  #     RSpec.describe UsersController, type: :controller do
  #       # ...
  #     end
  #
  # The different available types are documented in the features, such as in
  # https://relishapp.com/rspec/rspec-rails/docs
  config.infer_spec_type_from_file_location!

  # Filter lines from Rails gems in backtraces.
  config.filter_rails_from_backtrace!
  # arbitrary gems may also be filtered via:
  # config.filter_gems_from_backtrace("gem name")

  config.include Devise::Test::ControllerHelpers, type: :controller
  config.include Devise::Test::IntegrationHelpers, type: :request
end
```

# sources and documentation

[RSpec](https://github.com/rspec/rspec-rails)
[Devise](https://github.com/heartcombo/devise/wiki/How-To:-Test-controllers-with-Rails-(and-RSpec))
[FactoryBot](https://github.com/thoughtbot/factory_bot/blob/master/GETTING_STARTED.md#rspec)
[SimpleCov](https://github.com/simplecov-ruby/simplecov)
[Capybara](https://github.com/teamcapybara/capybara)
[Database Cleaner](https://github.com/DatabaseCleaner/database_cleaner)
[Pundit Matchers](https://github.com/chrisalley/pundit-matchers)
[WebMock](https://github.com/bblimke/webmock)







