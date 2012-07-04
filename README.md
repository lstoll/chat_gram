# ChatGram

ChatGram is a barebones Instagram realtime endpoint for posting images
to a chat service.  With it, you can...

* See when friends post pics -- in RealTime (tm)!

  ![](https://img.skitch.com/20110424-kpf4p1xhyejr9icffqg3pk5u5c.jpg)

* Search for recent Instagrams in a given lat/long!

  ![](https://img.skitch.com/20110424-fmj6khg6qq33ttatytkkdfj7s1.jpg)

  (Note: This requires custom location search => lat/long coordinates
integration).

## Installation

1. Clone the repo [from GitHub][gh].
2. `bundle install` to load the right dependencies.
3. `rake db:create` to create the database.
4. `bundle exec rackup config.ru` to start the server.

If you don't want to use Bundler or Rubygems, you can require
`chat_gram/app` manually and start it up like any other Rack
application.  Booya.

[gh]: https://github.com/technoweenie/instagram_campfire_hook

## Deployment

ChatGram is designed to be deployed on Heroku.  That means, config files
are [replaced with environment variables][env].  See
[`./chat_gram.rb`][envdesc] for the expected environment variables.

[env]: http://devcenter.heroku.com/articles/config-vars
[envdesc]: https://github.com/technoweenie/instagram_campfire_hook/blob/master/chat_gram.rb#L9

## Customizing

I tried to make the basic pieces as abstract as possible.  You should be
able to write custom chat service endpoints, or store your data in
CouchDB...

### Chat Services

The only service supported currently is [Campfire][cf].  I'd love to get
[Convore][cv] support at some point.

[cf]: https://campfirenow.com
[cv]: https://convore.com

### Data Store

The data store has a [simple API][dsapi] and can basically support anything.
Only basic DB support is included.

[dsapi]: https://github.com/technoweenie/instagram_campfire_hook/blob/master/lib/chat_gram/model.rb#L2-3

## Subscriptions

To activate the subscription webhook, run

    curl -F 'client_id=CLIENT-ID' \
     -F 'client_secret=CLIENT-SECRET' \
     -F 'object=user' \
     -F 'aspect=media' \
     -F 'verify_token=myVerifyToken' \
     -F 'callback_url=http://site/image' \
     https://api.instagram.com/v1/subscriptions/

## TODO

* Document startup env vars better
* Add yaml config file support.
* Finish Admin UI.
* Come up with a clever way to load other chat services or data stores.
* Bundle into a gem.
