# Passport.js authentication for GoCollab

[Passport](http://passportjs.org/) strategy for authenticating with [GoCollab](http://gocollab.com/) using the OAuth 2.0 API.

This module lets you authenticate using GoCollab in your Node.js applications.

By plugging into Passport, GoCollab authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-gocollab
```

## Usage

#### Configure Strategy

The GoCollab authentication strategy authenticates users using a GoCollab account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
var OAuth2Strategy = require("passport-gocollab").Strategy;

passport.use(new OAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "http://www.example.net/auth/gocollab/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'gocollab'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/gocollab',
	passport.authenticate('gocollab'));

app.get('/auth/gocollab/callback',
	passport.authenticate('gocollab', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [GoCollab](http://gocollab.com/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

