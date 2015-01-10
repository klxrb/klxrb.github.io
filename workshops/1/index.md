---
layout: article
title: "Workshop #1 Tutorial"
date: 2015-01-04T08:53:00+08:00
modified:
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
toc: true
share: false
---

<style>
.how-to { display: none; margin-top: 24px; }
.how-to + p { margin: 0; }
.no-margin-bottom { margin-bottom: 0; }
</style>

## Before you continue

Please make sure you have done the following :

- A [Github](https://github.com) account
- A [Digital Ocean](https://digitalocean.com) account & cash-in the voucher given earlier
- Have Ruby 1.9.3 installed  
- Have Redis Server installed locally
- Prepare SSH key for your machine


## Outline

In this tutorial we are building 2 simple apps - Shopping Cart & Customer Relationship Management (CRM) portal.

The Shopping Cart will have a catalogue of products, then customers can buy and sales will be captured. And in the end the customer's information is sent to the CRM.

In addition to that, we want to queue up the API requests so that the purchase process is not blocked / slowed down.

And finally, we need to write an automated deployment script to deploy both apps to their respective servers.


## Step 1: Creating the Shopping Cart

Estimate time: 20 mins

<p class="no-margin-bottom">
<input type="checkbox" id="c1_1"> Create Rails App with PostgreSQL database
[<a href="#" class="how-to-toggle">how ah?</a>]
</p>
<div class="how-to">
{% highlight bash %}
$ rails new shopping_cart --database=postgresql
$ cd shopping_cart
$ rake db:create
{% endhighlight %}
</div>

<input type="checkbox" id="c1_1"> Admin login using [Devise](https://github.com/plataformatec/devise)
[<a href="#" class="how-to-toggle">how ah?</a>]
<div class="how-to">
{% highlight ruby %} 
# Gemfile
gem 'devise' 
{% endhighlight %}

{% highlight bash %}
$ rails generate devise:install
$ rails generate devise Admin

$ rake db:migrate
{% endhighlight %}
</div>

<input type="checkbox" id="c1_2"> Setup [Upmin Admin](https://github.com/upmin/upmin-admin-ruby) on /admin
[<a href="#" class="how-to-toggle">how ah?</a>]  
<div class="how-to">
{% highlight ruby %} 
# Gemfile
gem 'upmin-admin'
{% endhighlight %}

{% highlight ruby %}
# config/routes.rb
mount Upmin::Engine => '/admin'
{% endhighlight %}
</div>

<input type="checkbox" id="c1_3"> Scaffold "Products" Model  
<input type="checkbox" id="c1_4"> Add some styles
[<a href="#" class="how-to-toggle">how ah?</a>]
<div class="how-to">
{% highlight ruby %} 
# Gemfile
gem 'foundation-rails'
{% endhighlight %}

{% highlight bash %}
$ rails g foundation:install
{% endhighlight %}
</div>

<input type="checkbox" id="c1_5"> Scaffold "Sales"  
<input type="checkbox" id="c1_6"> Product Checkout & Sales


## Step 2: Creating the CRM

Estimate time: 30 mins

<input type="checkbox" id="c2_1"> User login using [Devise](https://github.com/plataformatec/devise)
[<a href="#" class="how-to-toggle">how ah?</a>]
<div class="how-to">
{% highlight ruby %} 
# Gemfile
gem 'devise' 
{% endhighlight %}

{% highlight bash %}
$ rails generate devise:install
$ rails generate devise Admin

$ rake db:migrate
{% endhighlight %}
</div>

<input type="checkbox" id="c2_2"> Scaffold Customers Model
[<a href="#" class="how-to-toggle">how ah?</a>]
<div class="how-to">
{% highlight bash %} 
$ rails g resource Customer email:string first_name:string last_name:string address:string zipcode:string country:string
{% endhighlight %}
</div>

<input type="checkbox" id="c2_3"> Setup [Upmin Admin](https://github.com/upmin/upmin-admin-ruby)
[<a href="#" class="how-to-toggle">how ah?</a>]
<div class="how-to">
{% highlight ruby %} 
# Gemfile
gem 'upmin-admin' 
{% endhighlight %}

{% highlight ruby %}
# config/routes.rb
  mount Upmin::Engine => '/'
{% endhighlight %}
</div>

<input type="checkbox" id="c2_4"> "API Applications" Model  
<input type="checkbox" id="c2_5"> Setup API with [Grape](https://github.com/intridea/grape)  
<input type="checkbox" id="c2_6"> Setup API Documentation with [Grape-Swagger-Rails](https://github.com/BrandyMint/grape-swagger-rails)  


## Step 3: Integrating with API

Estimate time: 20 mins

<input type="checkbox" id="c3_1"> Generate API token for Shopping Cart app   
<input type="checkbox" id="c3_2"> Use API token to send customer data to CRM  
<input type="checkbox" id="c3_3"> Setup [Rails Config](https://github.com/railsconfig/rails_config)  


## Step 4: Queue Up Jobs

Estimate time: 15 mins

<input type="checkbox" id="c4_1"> Setup [Sidekiq](http://sidekiq.org/)  
<input type="checkbox" id="c4_2"> Use [Sidekiq](http://sidekiq.org/) to queue up jobs  


## Step 5: Setup Digital Ocean

Estimate time: 15 mins

<input type="checkbox" id="c5_1"> Generate / Get public SSH Key for machine  
<input type="checkbox" id="c5_2"> Add SSH Key  
<input type="checkbox" id="c5_3"> Create two (2) 14.04 x64 Ubuntu droplets with private networking


## Step 6: Prep the Servers

Estimate time: 20 mins

<input type="checkbox" id="c6_1"> Install [rbenv](https://github.com/sstephenson/rbenv) with [ruby-build](https://github.com/sstephenson/ruby-b id="c6_1"uild)  
<input type="checkbox" id="c6_2"> Install PostgreSQL  
<input type="checkbox" id="c6_3"> Install Redis Server  
<input type="checkbox" id="c6_4"> Security tweaks: change SSH port and disable root access


## Step 7: Deployment

Estimate time: 15 mins

<input type="checkbox" id="c7_1"> Setup [Capistrano](https://github.com/capistrano/capistrano) with [Capistrano Rbenv](https://github.com/cap id="c5_1"istrano/rbenv) + [Capistrano Sidekiq](https://github.com/seuros/capistrano-sidekiq) + [Capistrano Unicorn Nginx](https://github.com/capistrano-plugins/capistrano-unicorn-nginx)  
<input type="checkbox" id="c7_2"> Create & upload production settings  
<input type="checkbox" id="c7_3"> Finally ... Deploy Live !!  



---

### Overall Progress: <span id="progress">0</span>%

<script src="{{ site.url }}/js/vendor/jquery.storageapi.min.js"></script>
<script>
$(function(){
  ns = $.initNamespaceStorage('klxrb_ruby_workshop_1');
  storage = ns.localStorage;

  checked_items = storage.get('checked_items');

  function recheck(){
    if(checked_items.length > 1){
      $(checked_items.join(',')).prop('checked', true);
    }
  }

  function recalculate(){
    $('#progress').html(parseInt($('input[type=checkbox]:checked').length / $('input[type=checkbox]').length * 100));
  }

  function savestate(){
    checked_items = []
    $('input[type=checkbox]:checked').each(function(){
      checked_items.push('#' + $(this).prop('id'))
    })
    storage.set('checked_items', checked_items);
  }

  if(typeof checked_items === 'undefined'){
    checked_items = [];
  }else{
    recheck();
  }
  
  $('input[type=checkbox]').change(function(){
    recalculate();
    savestate();
  })

  recalculate();

  $('a.how-to-toggle').click(function(){
    $(this).parents('p').next('.how-to').toggle()
    return false;
  })
  
});

</script>

