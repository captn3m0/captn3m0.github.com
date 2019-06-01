---
layout: post
title: Cleaning up Google Purchases
---

The [Google Purchase History](https://www.cnbc.com/2019/05/17/google-gmail-tracks-purchase-history-how-to-delete-it.html) feature has been doing rounds recently. In case you missed it, go to <https://myaccount.google.com/purchases> right now and make sure you are logged in with your personal gmail account.

For me it lists purchases going as far back as 2014, which include:

1. All of my Amazon Purchases
2. Flipkart purchases
3. Gifts I've bought for others on various platforms
4. All my iCloud purchases
5. Google Playstore purchases as well, of course

While this isn't shocking in the least, I was surprised, because as a Infosec professional, I've disabled all of google's invasive tracking features:

1. All my Activity Controls are paused.
2. Google Location history is disabled for my account.
3. I have [Shared endorsements](https://myaccount.google.com/shared-endorsements) turned off.
4. Ad personalization is turned off.
5. I used to run with the [Protect my Choices](https://addons.mozilla.org/en-US/firefox/addon/protect-my-choices/) extension till a while back to avoid targeted advertising.

Regardless, the Google purchases page had hundreds of results, going back half a decade. Google currently does not offer a way to delete collected purchases directly, or to pause this collection in any way. The only way is to find the emails that Google scanned, and delete them.

For me, the following searches on Google gave decent results:

```
from:"no_reply@email.apple.com" subject:Invoice
from:auto-confirm@amazon.in
from:no-reply@flipkart.com
from:noreply@snapdeals.co.in
from:order-update@amazon.in
from:payments-messages@amazon.in
from:return@amazon.in
from:ship-confirm@amazon.in
from:shipment-tracking@amazon.in
```

Note that deleting the email doesn't seem to be sufficient either, you need to clear your Trash, and then wait for a while before the system refreshes.

Google seems to be picking up _all kinds of emails, including_:

1. Invoices
2. Shipment Confirmations / Updates
3. Return confirmations
4. Payment Confirmations
5. Order Cancellations
6. Payment Failures

What this means is that you could have initiated a payment on Amazon, failed it, and Google would still start to show it in your Purchase History.

## Warning about Deletions

I've already switched away from Amazon/Flipkart emails from my Gmail. But deleting invoices from your inbox isn't always the best idea. Most websites will let you re-download invoices (Amazon/Flipkart do), but take care not to delete any necessary emails that you might need for warranty claims later.
