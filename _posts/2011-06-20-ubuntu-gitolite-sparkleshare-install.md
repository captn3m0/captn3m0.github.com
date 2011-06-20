---
title: Setting Up Sparkleshare Server using Gitolite and Ubuntu
layout: post
---
##Introduction
Everybody seems to be all about open-source cloud-backup and sync solutions now-a-days. The hype is all around the cloud, they say. However cloud is just a stupid [concept for sales people][1], that I prefer to avoid. However people are coming up with all kinds of crazy ideas to create their own [dropbox][c1] [clones][c2]. A few similar services include [SpiderOak][so], [Ubuntu One][u1], [Sugar Sync][ss], and [Wuala][]. However, not all of them are compatible with Linux (unlike Dropbox, which is). 

##Comparision
So here's a minor comparision of some famous clients :

* **Dropbox** : Cuurent Leader, offers everything from sync, collaboration, sharing, public links, upgradable storage and is *the de-facto* client for synchonization tasks. However there have been a few issues regarding its privacy issues recently.
* **Ubuntu One** : Ubuntu One is Ubuntu's fighting offering to Dropbox. Its excellent, with an open source api, that allows one to create applications for the Ubuntu One platform very easily. However, the server-side of Ubuntu-One is still closed source, which means you cannot setup it on your own servers (similar to dropbox). Canonical has hinted that it might be made open source in the future.
* **Wuala** : is a file-backup network where you trade your own hard disk space for extra storage. This allows wuala to offer higher space at a much lower offering rate. 
* **SpiderOak** : I'm using this currently along with SparkleShare and Dropbox. It has proven to be very robust, allowing me to backup almost anything to its servers. I've got a 5GB account which is more than enough for me till now. Its very powerful interface allows one to control each and every aspect of your backup/sync/share process. Also it boasts of a true-privacy feature, meaning that all your documents are encrypted before being sent to dropbox. It also means that you can only reset your password from your own computer.

Take a look at <http://en.wikipedia.org/wiki/Comparison_of_file_synchronization_software> for a better comparision of several other services as well.

#Installing SparkleShare using gitolite
This is a simple tutorial on running your own sparkleshare server as a hosting server. Note, that this implementation should ideally be built as a separate module for sparkleshare-admin, which is still under works as of writing. Sparkleshare's basic concept is to use git repositories as storage places. In case you don't know what git is, I'd recommend [this guide][git] for more details. In short it is an awesome revisioning system for use by anyone managing code(or content for that matter as well). It allows you to keep track of what is happening with your directory, and revert back to earlier versions (among **several** other things). 

Sparkleshare asks you to setup a git-server somewhere and use it as a remote storage system. It offers out of the box support for git hosting providers [github][gh] and [gitorious][gi]. It also allows you to add your own custom servers as well. Enough description, lets get down to some work :

###Setup Gitolite
####Assumptions :
1. You are running a stable Linux OS (Fedore/Debian/Ubuntu etc)
2. user@host1 is your own computer
3. user2@host2 is the primary computer where you intend to start the server
4. The gitolite username is sparkle

{% highlight bash linenos %}
#On your host machine (which will be remote admin to the git share)
ssh-copy-id user2@host2:/tmp/user.tmp
#should not ask for password:
ssh user2@host2
sudo apt-get install gitolite 
sudo dpkg-reconfigure /tmp/user.pub
#Configuration Options may vary, but remember the gitolite user name that you specified
logout #Come back to your own computer
git clone sparkle@host2:gitolite-admin 
#Should work, or else you did something wrong. Go read the [gitolite docs](http://sitaramc.github.com/gitolite/doc/)
cd gitolite-admin
nano conf/gitolite.conf
{% endhighlight %}

###Setup WildRepos
Edit the file and add the following lines at the bottom :

{% highlight perl %}
repo	share/[a-z0-9]{6}
	C	=   @all
	RW+	=   CREATOR
{% endhighlight %}

Now we need a method to allow anyone to create git repositories on the server. This is accomplished via Gitolite's very powerful Wildcard Repositories feature. 
{% highlight linenos bash %}
#Login back to server
ssh user2@host2
#Since we are using package install method, sparkle's password needs to be set
sudo passwd sparkle
su - sparkle
nano .gitolite.rc
#search for $GL_WILDREPOS and set it to 1
logout
#Now we push our admin repo to add the wildrepo settings
#you're still inside the gitolite-admin directory, right
git push
{% endhighlight %}

###Setup Client
Now, your server is all setup, but there is still stuff to be done :
{% highlight bash linenos %}
#On user1@host1
mkdir -p ~/.ssh
sudo add-apt-repository ppa:warp10/sparkleshare
sudo apt-get update
sudo apt-get install sparkleshare libwebkit1.1-cil git-core
sparkleshare start &
sparkleshare stop
{% endhighlight %}
When you run sparkleshare for the first time, it asks you for a few things, including your email-id. Fill in those details, but do not setup your repository yet. You need to first allow your sparkleshare account access to gitolite.
{% highlight bash %}
cd ~/.config/sparkleshare
ls #Should reveal files called sparkleshare.email.key and sparkleshare.email.key.pub
cp sparkleshare.email.key.pub /path/to/gitolite-admin/keydir/
cd /path/to/gitolite-admin/
git commit -am "Added sparkleshare client1"
git push
{% endhighlight %}
Now if all goes well, you'd have allowed acess to gitolite for this user. We now need to re-run the sparkeshare setup again. Find it in your Applications. Now when it asks you to fill a repository path, type in the following details :

{% highlight yaml %}
Server: ssh://sparkle@host2
Path: /share/fh73ah
{% endhighlight %}

Please take care of the slashes, otherwise sparkleshare fails to recognize it as a valid ssh address. Instead of fh73ah, you can type any alphanumeric string of 6 characters. You can change this in your gitolite-admin conf.

After your first sync is complete (in which it tries to clone your existing repo, and gitolite creates it for you), you can find a folder called Sparkleshare in your home directory. This contains all your personal sparkleshares, including your first one. Put in any content inside the fh73ah and it would be automatically synchronized.

##Conclusion
The best thing about sparkleshare is that you can use your own server under your own rules. I've synced 143GB via Sparkleshare so far, and it has been working excellent so far. It takes a complete history, takes care of moves (git) and allows you to keeo huge backups easily. Just drag and drop, and forget. If you want to sync already existing folders, just drag them , and alt+drop them inside the shared folder. This way a sym-link gets created, which refers to the original directory. The sparkleshare folder on my computer takes up hardly a few kbs, but syncs worth 150gb. 

This method is only useful if you need to manage multiple accounts on the same host. Otherwise, you can refer to this [excellent post](http://www.webupd8.org/2011/03/set-up-sparkleshare-with-your-own.html) on webupd8 for instructions to install it to a single user system (which does not involve the complication of gitolite). I've been looking for some gitolite management scripts (I've written a few as well) which would allow one to easily add their own ssh keys. This way anyone can easily setup accounts on the system. However, as of now, this is just a dream.


[1]: http://everythingsysadmin.com/2011/06/avoid-using-the-term-cloud-com.html
[c1]: http://fak3r.com/geek/howto-build-your-own-open-source-dropbox-clone/
[c2]: http://www.rubyinside.com/rubydrop-a-dropbox-clone-in-ruby-3968.html
[so]: https://spideroak.com/
[u1]: https://one.ubuntu.com/
[ss]: https://www.sugarsync.com/
[Wuala]: http://www.wuala.com/
[git]: https://git.wiki.kernel.org/index.php/GitFaq
[gh]: https://www.github.com
[gi]: http://gitorious.org/

