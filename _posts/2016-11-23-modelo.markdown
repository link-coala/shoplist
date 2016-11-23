---
layout: post
title:  "modelo de la aplicacion"
date:   2016-11-23 13:43:29 +0000
categories: jekyll update
---

routes.rb
{% highlight ruby %}
Rails.application.routes.draw do
  get 'orders/create'
  get 'orders/new'
  get 'products/home'
  root 'products#home'
     resources :products do
       resources :orders   
end
end
{% endhighlight %}
orders_controller.rb
{% highlight ruby %}
class OrdersController < ApplicationController
def new
  @order = Order.new
  @line_item = LineItem.all
  @product = Product.all
end
def create
   @order = Order.new(order_params)
  if @order.save
  redirect_to @order
  else
    render 'new'
  end
 end
end
{% endhighlight %}
app/views/orders/new.html.erb
{% highlight html %}

<%= form_for :order, url: orders_new_path do |f| %>
  <p>
    <%= f.label :delivery_address %><br>
    <%= f.text_field :delivery_address %>
  </p>
 
  <p>
    <%= f.submit %>
  </p>
 
<% end %>
{% endhighlight %}

