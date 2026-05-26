## Stack
Rails 8.1.3 sample todo app using SQLite via the `sqlite3` gem.
Views use ERB layouts/partials, Hotwire Turbo + Stimulus through importmap, Propshaft assets, and Jbuilder for JSON views.
Tests use Rails' built-in Minitest with fixtures, controller tests, model tests, and Capybara/Selenium system tests.
Background jobs use Active Job with Solid Queue; Solid Cache and Solid Cable are also configured.

## Commands
Setup: `bin/setup` or `bin/setup --skip-server`.
Run locally: `bin/dev` or `bin/rails server`.
Test: `bin/rails test` and `bin/rails test:system`.
Lint/security: `bundle exec rubocop` and `bin/brakeman`.

## Conventions
Use standard Rails naming: singular models like `Todo`, plural controllers like `TodosController`, and RESTful routes in `config/routes.rb`.
Keep shared view markup in partials under `app/views/<resource>/_*.html.erb`; JSON response templates live beside them as `.json.jbuilder`.
Controllers currently respond with HTML and JSON using `respond_to`; add Turbo Stream responses only when the view flow needs them.
No authorization layer exists yet; if added, keep checks centralized in controllers or a dedicated policy layer instead of scattering them through views.

## Don'ts
Do not add new gems or JavaScript packages without approval.
Do not put inline JavaScript in ERB templates; use Stimulus controllers and importmap-managed modules.
Do not skip CSRF protection with `skip_before_action :verify_authenticity_token`.
Do not seed real user data; use `db/seeds.rb` only for safe sample data.

## Security
Never write, log, echo, commit, or expose secrets, API keys, `.env` values, `config/master.key`, or production credentials.
Never use `eval` or dynamic code execution on user-controlled input.
Never use `html_safe` or `raw` with untrusted input; rely on Rails escaping by default.
Use Active Record and parameterized queries; never string-interpolate user input into SQL.
Do not disable CSRF protection, Rails mass-assignment protections, or Devise session checks if Devise is added later.
