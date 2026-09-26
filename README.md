# Spotiforum

A Ruby on Rails social forum for music lovers: users post short (tag-based) messages, like/favourite/comment on them, and can log in with Spotify or Google to show off their favourite song/artist. Includes moderation tools (warnings, bans, blacklist) and an admin role.

## Stack

- Ruby 2.7 / Rails 6.1, SQLite3, Webpacker
- **Devise** for authentication (+ **omniauth-spotify** / **omniauth-google-oauth2** for social login)
- **Canard** for roles/permissions
- **rspotify** to query the Spotify API (favourite song/artist, playlists)
- **Lockbox** to encrypt sensitive fields (e.g. Spotify username)
- RSpec + Cucumber/Capybara for testing

## Structure (`spotiforum/`, the Rails app root)

```
app/models/       # User, Post, Comment, Like, Favourite, Warn, Blacklist
app/controllers/  # posts, comments, likes, favourites, warns, blacklists, users, profiles, pages
app/views/        # one folder per resource above
config/routes.rb  # community feed, post like/favourite/warn/ban, Spotify playlist actions, Devise auth
db/               # migrations & schema
spec/, test/, features/   # RSpec, Minitest and Cucumber suites
```

## Domain rules (enforced via custom validators on `User`)

- A favourite song/artist can only be set if the user logged in with Spotify.
- Google and Spotify login are mutually exclusive; admins can use neither.
- Non-Spotify/non-Google users must set a password.
- Blacklisted emails cannot register.

## Setup

```bash
cd spotiforum
bundle install
yarn install
rails db:create db:migrate
rails server
```

Spotify and Google OAuth credentials need to be configured (e.g. via `config/initializers/devise.rb` / environment variables) for social login to work.

## Authors

- Gaia Rossi
- Alessio Vernarelli
- Beatrice Vinciguerra 