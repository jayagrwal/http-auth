# http-auth
[Node.js](http://nodejs.org/) package for HTTP basic and digest access authentication.

## Installation

Via git (or downloaded tarball):

```bash
$ git clone git://github.com/gevorg/http-auth.git
```
Via [npm](http://npmjs.org/):

```bash
$ npm install http-auth
```	
## Example of usage
```javascript
/**
 * Requesting new authentication instance.
 */
var digest = auth({
	authRealm : 'Private area.',
	authList : ['Shi:many222', 'Lota:123456']
});

/**
 * Creating new HTTP server.
 */
http.createServer(function(req, res) {
	// Apply authentication to server.
	digest.apply(req, res, function() {
		res.end('Welcome to private area!');
	});
}).listen(1337);
```
## Example of loading list of users from file
```javascript	
/**
 * Requesting new authentication instance.
 */
var digest = auth({
	authRealm : 'Private area.',
	authFile : __dirname + "/users.htpasswd"
});

/**
 * Creating new HTTP server.
 */
http.createServer(function(req, res) {
	// Apply authentication to server.
	digest.apply(req, res, function() {
		res.end('Welcome to private area!');
	});
}).listen(1337);
```	
## Example with [express framework](http://expressjs.com/) integration
```javascript
/**
 * Requesting new authentication instance.
 */
var digest = auth({
	authRealm : 'Private area.',
	authList : ['Shi:many222', 'Lota:123456']
});

/**
 * Handler for path with authentication.
 */
app.get('/', digest.apply, function(req, res) {
	res.send('Welcome to private area!');
});
```
## Configurations

 - `authRealm` - Authentication realm.
 - `authFile` - File where user details are stored in format **{user:pass}**.
 - `authList` - List where user details are stored in format **{user:pass}**, ignored if `authFile` is specified.
 - `authType` - Type of authentication, may be **basic** or **digest**, optional, default is **digest**.
 - `algorithm` - Algorithm that will be used for authentication, may be **MD5** or **MD5-sess**, optional, default is **MD5**. Only for **digest** `authType`.

## Dependencies

 - **[node-uuid](https://github.com/broofa/node-uuid/)** - Generate RFC4122(v4) UUIDs, and also non-RFC compact ids.

## Issues

You can find list of issues using [this link](http://github.com/gevorg/http-auth/issues).

## License

(The MIT License)

Copyright (c) 2011 Gevorg Harutyunyan <i@gevorg.me>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the **Software**), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED **AS IS**, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.