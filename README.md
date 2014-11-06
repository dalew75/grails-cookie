This plugin makes dealing with cookies easy. Provides an injectable service and tag to easily get, set, and delete cookies with one line.

## Installation

To install the cookie plug-in just add to `BuildConfig.groovy`:
```groovy
compile ':cookie:0.51'
```
Or install via command line:
```
grails install-plugin cookie
```

## Configuration

You can configure how long the default cookie age will be (in seconds) when not explicitly supplied while setting a cookie.
```groovy
grails.plugins.cookie.cookieage.default = 86400 // if not specified default in code is 30 days
```
## Usage

The cookie plug-in extends the request and response objects found in controllers, filters, etc to allow the following:

Example of setting a new cookie: (this sets a cookie with the name `username` to the value `cookieUser123` with a expiration set to a week, defined in seconds)
```groovy
response.setCookie('username', 'cookieUser123', 604800)
```
OR
```groovy
response.setCookie('username', 'cookieUser123') // will use default age in Config (or 30 days if not defined)
```
To get the cookie value:
```groovy
request.getCookie('username') // returns 'cookieUser123'
```
To delete the cookie:
```groovy
response.deleteCookie('username') // deletes the 'username' cookie
```

## Usage by calling CookieService directly

The cookie plug-in provides a `CookieService` that can be used anywhere in your Grails application.
To use `CookieService`, declare a dependency injection:
```groovy
def cookieService
```
Setting a new cookie:
```groovy
cookieService.setCookie('username', 'cookieUser123', 604800)
```
OR
```groovy
cookieService.setCookie('username', 'cookieUser123') // will use default age in Config (or 30 days if not defined)
```

To creat a cookie with alphanumeric value,
```groovy
// The second parameter here defines the size of the random aphanumeric string size [a-z A-Z 0-9]
// So the cookie will be something like => username: 'LzNN0kbsELzXOqXQEJnRc8l........'
// will use default age in Config (or 30 days if not defined)
cookieService.setCookie('username', 128) 
```
Getting the cookie value:
```groovy
cookieService.get('username') // returns 'cookieUser123'
```
Deleting the cookie:
```groovy
cookieService.delete('username') // deletes the 'username' cookie
```

## Tag Lib (deprecated)

You can also get a cookie value with a tag:
```xml
<cookie:get name='username' />
```
**Note:** Since 0.5 this tag is deprecated and will be removed in next releases. Use `<g:cookie/>` tag instead.

## Notes

In the 0.3 release a big issue was fixed that now sets the cookie's path to the root `/` context.
Otherwise it was setting the path to the same as the controller/service that triggered it.
Most users I believe will want this behavior. If setting the path is desired, that can be accomodated.
Please contact me or do a pull request if you'd like that.

## Demo
You can check out [demo here](https://github.com/stokito/grails-cookie-demo)
