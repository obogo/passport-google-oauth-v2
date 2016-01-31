# Passport-Google-OAuth2

> This is a fork was created because the current repository was not being maintained and would not work properly with Google OAuth2.

[Passport](http://passportjs.org/) strategies for authenticating with OAuth 2.0.

This module lets you authenticate using Google in your Node.js applications.
By plugging into Passport, Google authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

The client id and client secret needed to authenticate with Google can be set up from the developer's console [Google Developer's Console](https://console.developers.google.com/project).

## Install

    $ npm install passport-google-oauth2

## Usage of OAuth 2.0

#### Configure Strategy

The Google OAuth 2.0 authentication strategy authenticates users using a Google
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

```Javascript
var GoogleStrategy = require('passport-google-oauth').OAuth2Strategy;

passport.use(new GoogleStrategy({
    clientID: GOOGLE_CLIENT_ID,
    clientSecret: GOOGLE_CLIENT_SECRET,
    callbackURL: "http://127.0.0.1:3000/auth/google/callback"
  },
  function(accessToken, refreshToken, profile, done) {
    User.findOrCreate({ googleId: profile.id }, function (err, user) {
      return done(err, user);
    });
  }
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'google'` strategy, to
authenticate requests.
Authentication with Google requires an extra scope parameter.  For information, go [here](https://developers.google.com/accounts/docs/OpenIDConnect#scope-param).

For example, as route middleware in an [Express](http://expressjs.com/)
application:

```Javascript
app.get('/auth/google',
  passport.authenticate('google', { scope: 'https://www.googleapis.com/auth/plus.login' }));

app.get('/auth/google/callback',
  passport.authenticate('google', { failureRedirect: '/login' }),
  function(req, res) {
    // Successful authentication, redirect home.
    res.redirect('/');
  });
```

## Examples

For a complete, working example, refer to the [OAuth 1.0 example](https://github.com/jaredhanson/passport-google-oauth/tree/master/examples/oauth)
and the [OAuth 2.0 example](https://github.com/jaredhanson/passport-google-oauth/tree/master/examples/oauth2).

## Tests

    $ npm install --dev
    $ make test

[![Build Status](https://secure.travis-ci.org/jaredhanson/passport-google-oauth.png)](http://travis-ci.org/jaredhanson/passport-google-oauth)

## Credits

  - [Jared Hanson](http://github.com/jaredhanson)
  - [Isman Usoh](https://github.com/isman-usoh)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2012-2013 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>
