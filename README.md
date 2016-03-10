meteor-force-ssl
================


Meteor Atmosphere page
https://atmospherejs.com/lsun/force-ssl

To install
```
meteor add lsun:force-ssl
```


This package redirects insecure connections to secure connection. Modified version of Meteor's force-ssl package (https://github.com/meteor/meteor)

The difference with this package and the original one supplied by meteor development group (mdg) is that this package checks for an expanded list of IP addresses in order to determine if the app is being served from a local host.

ie. 

original only checks for 127.x.x. pattern
https://github.com/meteor/meteor/blob/release/METEOR%400.9.4/packages/force-ssl/force_ssl_server.js
```

// Determine if the connection is only over localhost. Both we
  // received it on localhost, and all proxies involved received on
  // localhost.
  var localhostRegexp = /^\s*(127\.0\.0\.1|::1)\s*$/;
  var isLocal = (
    localhostRegexp.test(remoteAddress) &&
      (!req.headers['x-forwarded-for'] ||
       _.all(req.headers['x-forwarded-for'].split(','), function (x) {
         return localhostRegexp.test(x);
       })));


```

The modified version from lsun checks for a match with these values

````

@isPrivateAddress = (address) ->
	return true if /^\s*(127\.0\.0\.1|::1)\s*$/.test address
	return true if /^\s*(10\.\d+\.\d+\.\d+)\s*$/.test address
	return true if /^\s*(192\.168\.\d+\.\d+)\s*$/.test address
	return true if /^\s*(172\.(1[6-9]|2[0-9]|3[01])\.\d+\.\d+)\s*$/.test address
	return false
	
	
````
