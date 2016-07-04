---
layout: post
title:  "Making your Rails app work on Java"
date:   2009-09-26 22:16:20
categories: java jdbc jruby rails ruby software
---
So you’ve written a Rails app and you want to show it off to your boss at work because you know that it will impress them. Problem is that your company only uses Java and won’t consider it for their production environment if it can’t be deployed under a JVM. Let’s go:

* Install [JRuby](http://jruby.org)
* Install the required gems for Ruby on Rails to work with JRuby

`jgem install mongrel activerecord-jdbcsqlite3-adapter rails`

* Install the gems particular to your application

`jruby -S rake gems:install`

* Update your database.yml file, prefixing your adapter with jdbc

{% highlight yaml %}
development:
  adapter: jdbcsqlite3
  database: db/development.sqlite3
  pool: 5
  timeout: 5000
{% endhighlight %}

* Start your JVM

`jruby script/server`

* Demonstrate
* Sit back and wait for promotion
* Some notes on whats going on above:

Detailed installation instructions for JRuby can be found on their [wiki](http://kenai.com/projects/jruby/pages/GettingStarted).

The `jruby -S` rake command is very important as the -S switch ensures that the rake command is sourced from the JRuby home, not the system path which would contain a native Ruby install

[ActiveRecord-JDBC](http://kenai.com/projects/activerecord-jdbc/) can handle most any database you can think of in a corporate environment.

If you wish to use another database, there are some gems already pre-packaged, more details on the [github page](http://github.com/nicksieger/activerecord-jdbc-adapter).