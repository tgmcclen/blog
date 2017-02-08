---
title:  "Getting started with Heroku and Rails 3.1"
date:   2011-11-16 22:16:20
categories: cloud git heroku rails ruby software
---
Pre-requesites:

* [RVM](https://rvm.io/) on your local machine with Ruby 1.9.2
* [Heroku](http://heroku.com/) account

Switch to the 1.9.2 version of Ruby, install the rails and heroku gems, create your rails 3.1 application

{% highlight sh %}
$ rvm 1.9.2
$ gem install rails
$ gem install heroku
$ rails new tickets
$ cd tickets
{% endhighlight %}

Add in the nifty-generators gem:

/Gemfile
gem "nifty-generators", :group => :development
Terminal
$ bundle install
Generate the layout

Terminal
$ rails generate nifty:layout
Now make compatible with Rails 3.1 asset pipeline (assuming this is only temporary until gem is updated for Rails 3.1)

Rename /public/stylesheets/application.css to nifty.css and move to the /app/assets/stylesheets dir
Delete /public/stylesheets
Update javascript to use “application” instead of :defaults

/app/views/layouts/application.html.erb
<%= javascript_include_tag "application" %>
Generate the scaffold for a ticket, migrate the schema, and start the server to test locally at http://localhost:3000

Terminal
$ rails generate nifty:scaffold ticket name:string description:text

$ bundle exec rake db:migrate

$ rails server
Point to our tickets controller as default
Remove public/index.html
Update root route in routes.rb

/config/routes.rb
root :to => 'tickets#index'
Initialise the git repository and perform first commit

Terminal
$ git init

$ git add .

$ git commit -m "Initial commit"
Create the app on heroku using the cedar stack (its the only stack that currently supports Rails 3.1)

Terminal
$ gem install heroku

$ heroku create --stack cedar
Notice that there is now a new remote on our git repo

Terminal
$ git remote -v
Heroku uses postgresql by default, update gems

/Gemfile
gem 'sqlite3', :group => :development

gem 'pg', :group => :production
Terminal
$ bundle install
Commit changes

Terminal
$ git add .

$ git commit -m "Updated database gems to cater for postgresql on Heroku"
Push app to heroku, migrate the schema on the server, and open a browser to see it running

Terminal
$ git push heroku master

$ heroku run rake db:migrate

$ heroku open
Installing the custom domain Add-on

Notice that it has a unique subdomain, lets give it our own sub-domain name through the Custom Domain add-on

Terminal
heroku add custom_domain

heroku domains:add tickets.passbyvalue.com
Add a CNAME record on the DNS for the preferred subdomain (note that top level domain DNS rules are different) that we want to use and now try it out!

<http://tickets.passbyvalue.com>

Tutorial: <http://devcenter.heroku.com/articles/custom-domains>

Jump into the console and see under the covers

`$ heroku run console`

Wow! How cool is that! My goal now is to give up my own VPS for hosting my Rails apps. I’m thinking that it come out cheaper using Heroku.

Note: there are some limitations that you need to be aware of. For example you have limited write access to the file system so if you want your users to upload images then you need to incorporate different cloud offerings for this to work, like Amazon S3. The paperclip gem has support for this. This gives an insight in how your thinking has to change when you start to leverage cloud services and augment them together. Something to discuss further another time…