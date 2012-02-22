---
layout: post
title: Making post requests with 'request' module in node.js
---

Was stuck at this for quite some time:

{% highlight javascript %}
var postData={
	a:1,
	b:2
};
require('request').post({
	uri:"http://example.com/test",
	headers:{'content-type': 'application/x-www-form-urlencoded'},
	body:require('querystring').stringify(postData)
	},function(err,res,body){
		console.log(body);
		console.log(res.statusCode);
});
{% endhighlight %}

This will make a post request to `http://example.com/test` with the querystring parameters in postData. Meaning if you are using PHP, you can see the variables in `$_POST` instead of parsing request body.

References:

- <https://gist.github.com/1360979>
- <https://github.com/mikeal/request>
