Encode Session IDs in URLs for Laravel 5-8 Projects (Transparent SID)
===================================================================

This module adds support for keeping session IDs (as normally stored in session cookies) to all URLs.
This is especially useful if your application runs in Iframe as some browser block cookies in those.
PHP already provides the `session.use_trans_sid` configuration value for this, but as Laravel 5 is implementing sessions in its on way, our module is necessary.

Compatibility
-------------

| Laravel Version | Package Version |
| --------------- | --------------- |
| 5.x - 6.x | 2.0 |
| 7+ | 3.0 |

Installation
------------

1. Install `imi/laravel-transsid` via composer.
2. In your `config/app.php` at `providers` replace 
    `'Illuminate\Session\SessionServiceProvider'` with `\iMi\LaravelTransSid\SessionServiceProvider::class` 
3. Add `\iMi\LaravelTransSid\UrlServiceProvider::class` at the end of the providers array
4. (optional) In your `app/Http/Kernel.php` add `'urlsession' => \iMi\LaravelTransSid\UrlSession::class` to the `$routeMiddleware` array.

Usage
-----

To use SessionIDs in URLs add the middleware `urlsession` (if you registered the middleware globally) or add the 
`\iMi\LaravelTransSid\UrlSession::class` class directly to your route or routegroup.

URLs generated with Laravel's URL function (for example `URL::to()`) will now have a session ID appended. 

If direct path's are or the `previous()` method is used, the SID is always added, because no route is known.
If you would like to generate URLs without a session ID, add a `NO_ADD_SID` parameter:

    {{ URL::to('/', ['NO_ADD_SID' => true]) }}

Warning
-------

Session IDs in URLs are easier to steal than a session cookie.

About Us
========

[iMi digital GmbH](http://www.imi.de/) offers Laravel related open source modules. If you are confronted with any bugs, you may want to open an issue here.

In need of support or an implementation of a modul in an existing system, [free to contact us](mailto:digital@iMi.de). In this case, we will provide full service support for a fee.

Of course we provide development of closed-source modules as well.
