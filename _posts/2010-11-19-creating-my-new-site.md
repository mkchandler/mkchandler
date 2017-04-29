---
layout: post
title: "Creating My New Site"
date: 2010-11-19
visible: 0
---

A couple months back I set out to create a new web site for myself.  All I really wanted was a place to post my writings about programming and other interests, as well as somewhere that connects all of the online communities I'm involved in.  I went through a few iterations of prototypes before I finally decided to build it using [Ruby][ruby].  I'm very new to Ruby, and thought that building my personal site would be a great way to jump in to the language.

I knew from the start that I wanted the design to by very minimalistic.  I envisioned something simple, mostly text based, that would be easy to read.  Along with the design of the site being simple, there is no reason the back-end of the site should not be the same.  I started out writing the site in C# using the [ASP.NET MVC 2][aspnetmvc] framework and a SQL database for storage.  This is what I use in my day job, so I was very familiar with it.  But I found out after a week or so of building it that it was becoming too large and complicated for my little site.  This was probably my own fault for "over-engineering" it, but I'm used to building large scale sites with that technology stack.  So after a couple weeks of tweaking and re-tweaking, I decided to look for something simpler, quicker, smaller, etc.  That's when I found [toto][toto]; and it was love at first sight.

[aspnetmvc]: http://asp.net/mvc/
[toto]: http://cloudhead.io/toto/
[ruby]: http://ruby-lang.org/

The toto Engine
---------------

I was flipping through some of my favorite blogs, getting ideas, when I came across a blog that was powered by toto.  I was not familiar with toto, so I decided to see what it was all about.  After reading the short description and the "getting started" guide, I knew that this was the perfect engine for my site.  There's no huge framework, no SQL database, and is only around 300 lines of code.

Toto is written in Ruby runs directly on top of [Rack][rack].  All articles are stored as individual txt files, and it uses the [YAML][yaml] format to get the title, author, post, etc. out of the file.  All this simplicity was exactly what I was looking for, and will allow me to put my focus on writing great articles and not worrying about an admin interface and all that jazz.

[rack]: http://rack.rubyforge.org/
[git]: http://git-scm.com/
[yaml]: http://yaml.org/

Designing the Interface
-----------------------

The default template for toto is called [dorothy][dorothy], which is a very minimalistic design.  This is what I started with, and for now have just made some very minor adjustments.  Most of my influence for the design is coming from the following blogs:

- <http://8164.org/>
- <http://stevelosh.com/blog/>
- <http://journal.uggedal.com/>
- <http://sirupsen.com/>

I believe these sites excel in their designs because of how easy it is to read the posts.  The site uses HTML5 elements for layout, but nothing too complex.  I will dive further into the design in a future post.

[dorothy]: https://github.com/cloudhead/dorothy

Hosting the Site on Heroku
--------------------------

[Heroku][heroku] is a Ruby hosting platform that offers many levels of scalability.  I'm running this site on a free account, but I could easily boost it if I started getting 10,000 hits a day (not expecting that to happen though, haha.)  Deployment to Heroku is done purely though Git, which means along with your hosting, all of your code and content (because your posts are just txt files) are source controlled!  Heroku has a very clean and easy API for managing your site, and makes deployment a breeze.

> *Note: I'm also hosting the source code on [GitHub][mkcgithub].  I will do a future post on the workflow that I use to push the source to both github and Heroku.*

There are also a ton of add-ons for your Heroku account.  Everything ranging from [Zerigo][zerigo] DNS management to [CouchDB][couchdb] hosting to [Memcached][memcached] distributed caching.  And of course there are a lot more, check them all out [here][addons].

[heroku]: http://heroku.com/
[mkcgithub]: https://github.com/mkchandler/mkchandler.com
[zerigo]: http://zerigo.com/
[couchdb]: http://couchdb.apache.org/
[memcached]: http://memcached.org/
[addons]: http://addons.heroku.com/

Setting up my Domain Name
-------------------------

Now I had a back-end up and running, a front started (though not yet completed), and all I needed to do was get my domain name pointed to my Heroku account.  Heroku makes this very simple by using their Custom Domains add-on.  I set up the Zerigo DNS add-on for DNS management.  All I had to do then was point my nameservers to the Zerigo nameservers.  I also wanted to make sure that you don't have to type the (obsolete) www (<http://no-www.org>), and if you do type the www subdomain, it redirects to my domain without the www.  This was very easy with Zerigo; all I had to do was set up a Redirect in their admin interface from www.mkchandler.com to mkchandler.com.

Conslusion
----------

So with all of that said, I still have a lot of work to do.  There are a couple changes to toto I would like to make, and I will continue to update the design over the next month or so.  Send your questions and comments to me on [twitter]!

[twitter]: http://twitter.com/mkchandler/
