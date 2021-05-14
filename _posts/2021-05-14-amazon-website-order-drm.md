---
layout: post
title: Amazon Order History Encryption Bypass
tags:
- amazon
- encryption
- csd
---

The Amazon US website allows you to export your Order History easily by visiting the "[Order History Reports](https://www.amazon.com/gp/b2b/reports)" page. No such option seems to exist for the Amazon websites for other countries. I was trying to write a simple scraper for the [Amazon India Order History Page](https://www.amazon.in/gp/your-account/order-history) to get the same data, and discovered something interesting: Amazon encrypts the Order history page, and decrypts it using client side cryptography[^1]. If you were to visit the page, and check the response HTML, you'd see something like this in the source code (fairly simplified):

```js
// Define encrypted content in JS
var payload = {
  "kid": "b70014",
  "iv": "/HenfXwYrGrrw8ff",
  "ct": "Wt78pPcibe8HAdVtoJ8+E9EGwt4IQYNghBMubBy7Zy/..."
}
// The HTML div to be populated with the decrypted HTML
var elementId = "csd-encrypted-889C1D02..";
// if client side decryption library failed to load
if (!window.SiegeClientSideDecryption) {
  window.location.href = "?disableCsd=missing-library";
  return;
}
// Decrypt and populate the div
SiegeClientSideDecryption.decryptInElementWithId(
  elementId, payload, {callSource: "now"}
);
```

The easiest way to scrape with such hurdles is often to just [run a complete browser](https://github.com/angrykoala/awesome-browser-automation) to scrape the site. The browser runs the javascript code with the decryption routine so you can scrape the actual content. However, it is much slower, and wastes CPU cycles - I try to avoid it if I can.

<aside><details markdown=1><summary>Aside: Click here for explanation of the decryption code</summary>
The server sends some HTML encrypted as a JSON payload (`ct` is truncated ciphertext in the snippet above), along with the IV and a Key ID. The `SiegeClientSideDecryption` library is then called to decrypt the payload and set the plaintext result as inner HTML of the elementID. The code redirects to a different URL in case the decryption library fails to load.
</details></aside>

I could have spent time to parse the encryption routine, extract the key and decrypt the payload. But I found a much simpler solution - Amazon offers an alternate URL which disables encryption. As a fallback, in case the decryption code fails, it adds a query parameter `?disableCsd=missing-library`. That disables the server side encryption entirely.

So if you're trying to scrape Amazon and stumped at the missing order history in the HTML, try visiting the following URLs instead:

- <https://www.amazon.in/gp/css/order-history?disableCsd=missing-library>
- <https://www.amazon.co.uk/gp/css/order-history?disableCsd=missing-library>
- <https://www.amazon.com/gp/css/order-history?disableCsd=missing-library>

Amazon also sets a cookie `csd-key=disabled` but I didn't experiment with that much.

[^1]: I'm hesitant to call this <a href="https://www.defectivebydesign.org/"><abbr title="Digital Restrictions Management">DRM</abbr></a>, but it might qualify as such.