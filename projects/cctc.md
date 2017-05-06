---
permalink: /reports/cctc/
layout: report
date: 2017-03-25
title: CCTC Report
---
## Challenge 1

### Task : Register and login with an email-id [John_Doe@somemailinator.com](mailto:John_Doe@somemailinator.com)

### Vulnerability/Vulnerabilities Identified

1.  Insufficient Validation performed for authentication
2.  Development code left in production

### Applicable root cause(s)

The code for approving a user was left inside resend.asp, allowing anyone to approve his/her own account easily by faking a request. This was probably done during development stage of the application, as a means of easy activation of accounts, but was left commented out in the javascript, leading to easy exploitation

There was insufficient validation performed in validating the user. There was no check performed to see if 1\. the user is logged in and 2\. the user is an admin user

Inspite of both these conditions being false, the user could approve any other email.

### Approach Adopted

After studying resend.asp and seeing the following javascript code :

```js
function submitted() {
  email = document.getElementById('email_id').value;
  if (email == '') {
    alert('Email Address cannot be empty');
    return false;
  } else {
    //boolean is_approved
    return true;
  }
  return false;
}

```

We tried to submit the form with another element, called "is_approved" with its value set to "true" and the user account was approved.

## Suggested Remediation

1.  Remove the approval code from `resend.asp`
2.  Remove the `is_approval` variable reference from resend.asp

The offensive code snippet for `(1)` above would be something like :

```php
<?php
if($_POST('is_approved')==true){
  $email_id = $mysqli->escape_string($_POST['email']);
  $mysqli->query("UPDATE users set approved=1 WHERE email_id = '$email_id'");
}
```

Similarly `(2)` above can be fixed by shortening the javascript validation code to :

```js
function submitted() {
  email = document.getElementById('email_id').value;
  if (email == '') {
    alert('Email Address cannot be empty');
    return false;
  } else {
    return true;
  }
  return false;
}
```

## Challenge 2

### Task : Find hidden credentials in the application and login with them

### Vulnerability/Vulnerabilities Identified

1.  Hidden Credentials left in application data

### Applicable root cause(s)

The credentials for the hidden user account were left in the images of various books. This was probably due to poor joke being played by the developers. Also possible is that the application developer was trying to leave himself a backdoor in the application.

### Approach adopted (steps with screenshots)

1.  After getting a hint of hidden credentials, we looked in various places and found certain books of importance ('Base64 Encoded', and `Secret`)
2.  We analyzed these book's covers and found that they contained base 64 encoded versions of a hidden username and password.
3.  We attempted to login with these credentials, and found that only one of them worked.

### Suggested remediation with sample code snippet

1.  Update the book cover picture of these books with the credentials removed.

## Challenge 3

### Task: Buy at least one copy of each book costing more than 800 credit points

### Vulnerability/Vulnerabilities Identified

1.  Insufficient Validation on user input
2.  Unnecessary user input ###Application Root Cause A user is allowed to specify the cost of the book while purchasing it. ###Approach adopted (steps with screenshots)
3.  We looked at the javascript code of `books.asp` where the purchase is made and found the following snippet :

```js
function purchase(bid, cost) {
    $.ajax({
        url: 'checkout.asp?book_id=' + bid + '&action=checkin',
        success: function(msg) {},
    });
    $.ajax({
        url: 'purchase.asp?book_id=' +
            bid +
            '&action=purchase&book_cost=' +
            cost,
        success: function(msg) {
            alert(msg);
            history.go(0);
        },
    });
}
```

4.  We found that the application was sending a get request to `purchase.asp` with the fields `book_id` , `purchase`, and `book_cost`.

5.  The application also sent a request to `checkout.asp` to make sure that the book was checked out (See Generic Vulnerability 1 for more details on this)

6.  We checked all the books and found the following books had cost above 800:

    1.  (66) : XPATH - 9245
    2.  (64) : WPA 2 - 2345
    3.  (35) : IT ACT 2008 - 2000
    4.  (56) : SQL Injection - 990
    5.  (59) : Symmetric Encryption - 888
7.  We performed a GET request to `purchase.asp?action=purchase&book_id=66&book_cost=-10000` allowing us to buy the first book in the list and raise our credits by 10000.

8.  The other books were bought with similar GET requests to the following urls : `purchase.asp?action=purchase&book_id=64&book_cost=0`
    `purchase.asp?action=purchase&book_id=35&book_cost=0`
    `purchase.asp?action=purchase&book_id=56&book_cost=0`
    `purchase.asp?action=purchase&book_id=59&book_cost=0`

### Suggested remediation with sample code snippet

Do not allow a user to specify cost for a book by himself.
**Sample Code Snippet** Change

```php
<?php
$cost = $_GET['cost'];
//Validation integer
$mysqli->query("INSERT INTO purchase(book_id,cost) VALUES($id,$cost)");
```

**to**

```php
<?php
$result = $db->query("SELECT cost from books where book_id = $id");
$row = $result->fetch_assoc();
$cost = $row['cost'];
$db->query("INSERT INTO purchase(book_id,cost) VALUES($id,$cost)");
```

## Challenge 5

### Vulnerability/Vulnerabilities Identified

1.  SQL Injection

### Applicable root cause(s)

The application does not validate the `book_id` field for a request to `checkout.asp` sufficiently

## Generic 1

### Vulnerability Identified

1.  Weak/Guessable Password ###Applicable Root Cause The password for the user `cctc` was very weak ###Approach adopted
2.  Running on the shell : `cd /home/ ls cctc student`
3.  We knew that there was a user called cctc on the system, so we tried guessing the password : `logout debian login: cctc Password: cctc`
4.  Also _all mail for root user is being forwarded to the `cctc` user_ since the directory `/var/mail/root` does not exist.
5.  `mail` command gave us access to all forwarded mail for `root` user (Attach Screenshot Here)

## Generic 2

### Vulnerability/Vulnerabilities Identified

1.  Client Side Script for Checkout ###Applicable root cause(s) A click on the purchase button is supposed to do two things :
2.  Checkout the book.
3.  Purchase the book.

It does so by sending out two requests to checkout.asp and purchase.asp

Both of these requests can be forged individually by an attacker.

Also **Async javascript code** is vulnerable

### Approach adopted (steps with screenshots)

1.  A person could purchase a book, without checking it in, by simply making a request to `purchase.asp`

The async code is given below :

```js
function purchase(bid, cost) {
    $.ajax({
        url: 'checkout.asp?book_id=' + bid + '&action=checkin',
        success: function(msg) {},
    });
    $.ajax({
        url: 'purchase.asp?book_id=' +
            bid +
            '&action=purchase&book_cost=' +
            cost,
        success: function(msg) {
            alert(msg);
            history.go(0);
        },
    });
}
```

A side-effect of using ajax in such a sensitive environment is that you do not control the order of requests performed. Here, a request to `purchase.asp` may get completed before `checkout.asp`, which may have caused problems if the code was written out properly.

### Suggested remediation with sample code snippet

Instead of the client sending out two requests, there should be a single request to `purchase.asp`, which should automatically checkin the book, before purchasing it. **Use:**

```php
<?php
//purchase.asp
$id = $_GET['book_id'];
checkout($id);
purchase($id);
```

**Instead of :**

```php
<?php
purchase($_GET['id']);
```
