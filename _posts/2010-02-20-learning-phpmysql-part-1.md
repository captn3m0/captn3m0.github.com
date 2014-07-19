---
layout: post
title: Learning PHP/mySQL Part 1
tags:
- learning
- php
status: publish
type: post
published: true
meta:
  _wpas_done_twitter: '1'
  _edit_last: '10777942'
---
Over the past 2 months, I’ve been learning PHP/mySQL as a great language. After helping out a lot of people, I’ve decided to write a tutorial on using PHP/mySQL to create a cool website. For the entire duration of this tutorial, this is the list of softwares we will be working with:

><a href="http://www.google.com/search?btnI=I'm Feeling Lucky&amp;q=XAMPP Server Lite version">XAMPP Server Lite version</a> (to get apache &amp; mySQL)  
><a href="www.mediafire.com/?4eemynbynjw" target="_blank">Dreamweaver CS4</a> (For Template Support). Alternatively use <a href="http://www.google.com/search?btnI=I'm Feeling Lucky&amp;q=Microsoft Expression Web 3">Microsoft Expression Web 3</a>.  
><a href="http://www.google.com/search?btnI=I'm Feeling Lucky&amp;q=Notepad++">Notepad++</a> (Its a cool editor)  
><a href="http://www.google.com/search?btnI=I'm Feeling Lucky&amp;q=PHP Manual">PHP Manual</a> (download the full html version)

The website we will be developing is called Artemis Fowl Files (AFF for short). It is a small website with several features that we shall develop over the length of the tutorial.

##Installing PHP &amp; mySQL using XAMPP


PHP is a server side scripting language. Which means that PHP is run on the web server itself. For example any PHP script running at Google.com will remain on the server, and not reach you (the client). By contrast, JavaScript runs on the client side, i.e. any JS code must be transmitted to the client before being executed.

This is how a basic PHP script actually runs:

>PHP source File –&gt; PHP Parser (running on the web server) –&gt; Becomes an HTML file –&gt; HTML File sent to Client

Which means that the PHP source file is run on the server, which converts the file to a pre-calculated html file, which is then sent to the client. Lets write some basic php coding.

    1:  <HTML>
    2:  <HEAD><TITLE>Sample PHP File</TITLE></HEAD>
    3:  <BODY>
    4:  <?php
    5:  echo "This is a sample PHP File";
    6:  ?>
    7:  </BODY>
    8:  </HTML>

The basic context of PHP is that the only code that is considered PHP is that covered between &lt;?PHP and ?&gt; blocks. Anything outside these is neglected and remains the same(i.e. it is not run on the server). The echo command sends the text string to the html file. All this means that the file received by the client will look like this:

    1:  <HTML><HEAD><TITLE>Sample PHP File</TITLE></HEAD>
    2:  <BODY>
    3:  This is a sample PHP File
    4:  </BODY>
    5:  </HTML>


This is what you will  get if you ran the script on a test server. But before doing that we must install XAMPP, and do some basic setup stuff.

Download, and Extract XAMPPlite.exe anywhere in your computer. Go to where you installed it and run setup_xampp.bat. This will automatically start the Apache Server, and the mysql Server by default. Also try tinkering with XAMPP-Control and see what runs it.

Now open your web browser (Firefox/Chrome is preferred) and open <a href="http://127.0.0.1">http://127.0.0.1</a>. This IP address is a loopback IP address and always refers to this computer itself (yours). Now you should see a XAMPP splash screen. Go ahead and explore. As of now, what you’ve achieved is this : Installed Apache and the mySQL server. Now we need to change the settings for mysql. Open <a href="http://127.0.0.1/security/xamppsecurity.php">http://127.0.0.1/security/xamppsecurity.php</a> and change the mysql root password(its blank by default). Also set a password on the xampp directory, so that others cant access these settings. Remember the mysql root password, for it will be useful later on.

Now comes the part where we actually sit down to write some code. We will be developing the mysql parts in the next segment. However we still need to do some other little things before we reach that part.

##Creating The Dreamweaver Template

Now, call me lazy, but I don’t like designing themes, and CSS for my websites. I usually use a free one. And for the rest of this tutorial, I assume you will do the same. We need to create a Dreamweaver website using a readymade CSS Template. To get a template head on to <a href="http://www.freecsstemplates.org">http://www.freecsstemplates.org</a>. I choose <a href="http://www.freecsstemplates.org/preview/reckoning" target="_blank">this</a> template. Feel free to choose anything. It does not really matter which, but take care not to download a three column template, because what we will be developing is quite basic.

Create a directory called artemis inside htdocs folder(found inside xampp). Extract the css template files to the artemis folder such that the index.html file is inside xampp\artemis . Now head to your browser and open <a href="http://127.0.0.1/artemis">http://127.0.0.1/artemis</a>.

If all went well, you should now see the template theme. Now we must convert this css template into a Dreamweaver template. Open the index.html file in  Dreamweaver. We have to mark certain areas that we intend to edit in each document as editable. For instance the top header in each document must remain the same and would not be editable. But the sidebar content may need to change as per each page on our site. Taking this further the footer will be the same for each page. To create an editable region, just select a sample text from the main text (the one on that looks like the blog entry) and right click –&gt;Templates-&gt;Create Editable Region.

Dreamweaver will give a warning that the current document will be converted to a template. That is what we want. Give a name to the region(lets call it ‘main’). Now delete everything other than this main region from the right column(ie the blog entry column. You may need to switch to the split view to cleanly delete the html markup.

Similarly create another editable region for the sidebar. Remember to delete everything else in the sidebar as well. Now there is something to Dreamweaver which requires you to create a “site” before you can create a template. So go to Site Menu and click on New Site. Choose a site name (Artemis) and enter the correct web address where you can access index.html (<a href="http://127.0.0.1/artemis">http://127.0.0.1/artemis</a> or <a href="http://localhost/artemis">http://localhost/artemis</a>). Tell Dreamweaver that you want to use a server technology (PHP mySQL). Choose edit and test locally(because we don’t yet have access to an external web server).

Once you’ve created a site, you can save the web template. (Ctrl S). Currently no templates exist in our web site, So we will create one and call it “main template”. If Dreamweaver asks you to update links, press yes.

Now we will create our basic home page using this template. Press Ctrl+N to create a new page. On the left choose “Page from Template”, Choose the site as Artemis, and the template as well. Press Create, and viola, we have our homepage. You may see that the heading, footer, and links are not changeable, because they’re not defined as “editable” in the template. However the regions you choose to be editable are marked as such. Try writing some basic text in the sidebar and in the main content screen, and then save the file as index.php.

Now open <http://127.0.0.1/artemis/> in your computer, and be greeted with your newest creation. It' is still, as of now, a static site, with links that don’t work and no dynamism, but we will make it better in the next part.

If you had trouble following this tutorial anywhere feel free to post comments, or tweet me @captn3m0. I will be happy to reply. Further if you feel that you missed something, here is my work for you to compare with:

//#todo add link to zip file here
