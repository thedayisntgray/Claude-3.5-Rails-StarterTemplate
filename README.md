
# Claude 3.5 Starter Prompt

I'm working on a Rails application that was created using the following process and specifications. Please assume this exact configuration when answering my questions:

1. Rails version: 7.0.8
2. Ruby version: 3.2.2
3. Database: PostgreSQL
4. CSS: Tailwind CSS (via tailwindcss-rails gem, not Yarn-based)
5. Authentication: Devise
6. Testing: RSpec with FactoryBot
7. Background processing: Sidekiq with Redis
8. Environment variables: Managed with dotenv-rails

Key files and their contents:

1. Gemfile:
```ruby
source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '3.2.2'

gem 'rails', '~> 7.0.8'
gem 'pg', '~> 1.1'
gem 'puma', '~> 5.0'
gem 'turbo-rails'
gem 'stimulus-rails'
gem 'jbuilder'
gem 'redis', '~> 4.0'
gem 'bootsnap', require: false
gem 'devise'
gem 'dotenv-rails'
gem 'sidekiq'
gem 'tailwindcss-rails'

group :development, :test do
  gem 'debug', platforms: %i[ mri mingw x64_mingw ]
  gem 'rspec-rails'
  gem 'factory_bot_rails'
end

group :development do
  gem 'web-console'
  gem 'rack-mini-profiler'
  gem 'spring'
end

group :test do
  gem 'capybara'
  gem 'selenium-webdriver'
  gem 'webdrivers'
end
```

2. config/routes.rb:
```ruby
Rails.application.routes.draw do
  devise_for :users
  root 'pages#home'
end
```

3. app/models/user.rb:
```ruby
class User < ApplicationRecord
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
end
```

4. app/views/layouts/application.html.erb:
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>MyApp</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag "tailwind", "inter-font", "data-turbo-track": "reload" %>
    <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
    <%= javascript_importmap_tags %>
  </head>

  <body>
    <%= render 'shared/flash' %>
    <%= yield %>
  </body>
</html>
```

5. app/assets/stylesheets/application.tailwind.css:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Custom styles go here */
```

Additional setup:
- RSpec is configured as the testing framework
- Sidekiq is set up to work with Redis for background job processing
- A basic PagesController with a home action exists
- Devise is installed and configured with a User model
- The application uses foreman for development (bin/dev script and Procfile.dev)
- A .env file exists for environment variables (not committed to version control)

When I ask questions or request features, please assume this configuration as the starting point. I'm looking for advice, code snippets, or guidance on how to extend this application or implement new features.
