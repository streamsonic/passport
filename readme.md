# Passport.js authentication for Soundtrap

[Passport](http://passportjs.org/) strategy for authenticating with [Soundtrap](https://soundtrap.net/) using the OAuth 2.0 API.

This module lets you authenticate using Soundtrap in your Node.js applications.

By plugging into Passport, Soundtrap authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-soundtrap
```

## Usage

#### Configure Strategy

The Soundtrap authentication strategy authenticates users using a Soundtrap account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
passport.use(new SoundtrapOAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "https://www.example.net/auth/soundtrap/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'soundtrap'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/soundtrap',
	passport.authenticate('soundtrap'));

app.get('/auth/soundtrap/callback',
	passport.authenticate('soundtrap', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [Soundtrap](http://soundtrap.net/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

