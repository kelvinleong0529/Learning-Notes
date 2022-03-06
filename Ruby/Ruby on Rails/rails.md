# **Ruby on Rails**
## **What is Rails?**
1. An extremely productive web-application framework.
2. Written in Ruby by David Heinemeier Hansson.
3. You could develop a web application at least ten times faster with Rails than you could with a typical Java framework.
4. An open source Ruby framework for developing database-backed web applications.
5. Configure your code with Database Schema.
6. No compilation phase required.

## **Full Stack Framework**
1. Includes everything needed to create a database-driven web application, using the Model-View-Controller pattern.
2. Being a full-stack framework means all the layers are built to work seamlessly together with less code.
3. Requires fewer lines of code than other frameworks
## **Convention over Configuration**
1. Rails shuns configuration files in favor of conventions, reflection, and dynamic runtime extensions.
2. Your application code and your running database already contain everything that Rails needs to know!

## **Metaprogramming**
Where other frameworks use extensive code generation from scratch, Rail framework uses Metaprogramming techniques to write programs. Ruby is one of the best languages for Metaprogramming, and Rails uses this capability well. Rails also uses code generation but relies much more on Metaprogramming for the heavy lifting.

## **Active Record**
Rails introduces the Active Record framework, which saves objects into the database. The Rails version of the Active Record discovers the columns in a database schema and automatically attaches them to your domain objects using metaprogramming.

## **Convention over configuration**
Most web development frameworks for .NET or Java force you to write pages of configuration code. If you follow the suggested naming conventions, Rails doesn't need much configuration.

## **Scaffolding**
You often create temporary code in the early stages of development to help get an application up quickly and see how major components work together. Rails automatically creates much of the scaffolding you'll need.

## **Built-in testing**
Rails creates simple automated tests you can then extend. Rails also provides supporting code called harnesses and fixtures that make test cases easier to write and run. Ruby can then execute all your automated tests with the rake utility.

## **Three environments**
Rails gives you three default environments: development, testing, and production. Each behaves slightly differently, making your entire software development cycle easier. For example, Rails creates a fresh copy of the Test database for each test run.

# **Framework**
When we set out to write a Rails Application, leaving aside the configuration and other housekeeping chores, we have to perform three primary tasks
1. **Describe and model your application's domain** => The domain is the universe of your application. The domain may be a music store, a university, a dating service, an address book, or a hardware inventory. So here you have to figure out what's in it, what entities exist in this universe and how the items in it relate to each other. This is equivalent to modeling a database structure to keep the entities and their relationship.
2. **Specify what can happen in this domain** => The domain model is static; you have to make it dynamic. Addresses can be added to an address book. Musical scores can be purchased from music stores. Users can log in to a dating service. Students can register for classes at a university. You need to identify all the possible scenarios or actions that the elements of your domain can participate in.
3. **Choose and design the publicly available views of the domain** => At this point, you can start thinking in Web-browser terms. Once you've decided that your domain has students, and that they can register for classes, you can envision a welcome page, a registration page, and a confirmation page, etc. Each of these pages, or views, shows the user how things stand at a certain point.
## **Ruby on Rails MVC Framework**
- **M**odel **V**iew **C**ontroller principle divides the work of an application into three separate but closely cooperative subsystems
1. **Model (ActiveRecord )**
   
It maintains the relationship between the objects and the database and handles validation, association, transactions, and more.
This subsystem is implemented in ActiveRecord library, which provides an interface and binding between the tables in a relational database and the Ruby program code that manipulates database records. Ruby method names are automatically generated from the field names of database tables.

2. **View ( ActionView )**

It is a presentation of data in a particular format, triggered by a controller's decision to present the data. They are script-based template systems like JSP, ASP, PHP, and very easy to integrate with AJAX technology.
This subsystem is implemented in ActionView library, which is an Embedded Ruby (ERb) based system for defining presentation templates for data presentation. Every Web connection to a Rails application results in the displaying of a view.

3. **Controller ( ActionController )**

The facility within the application that directs traffic, on the one hand, querying the models for specific data, and on the other hand, organizing that data (searching, sorting, messaging it) into a form that fits the needs of a given view.
This subsystem is implemented in ActionController, which is a data broker sitting between ActiveRecord (the database interface) and ActionView (the presentation engine).

![alt text](https://www.tutorialspoint.com/ruby-on-rails/images/rails-framework.gif)

# **Creating New Rails App**
- creates a bunch of files (readme etc) and initialize a GIT repository for us
- **Gemfile** allows us to specify the gems version that will be specifically used in the app
```CMD
rails new (project_name)

eg: rails new scheduled_tweets
```
## **Install the dependancies in Gemfile**
- **Gemfile** is like the **package.json** file in JavaScript, it specificies the gems and its version for an app
- If we run the command **"Bundle"**, it will find the **Gemfile**, read through it and install the necessary versions
```RUBY
bundle # run this command to find the Gemfile, and install all the dependancies required
```
- There are 3 environments, **Test, Development & Production**

# **Routes and Route Types**
```RUBY
Rails.application.routes.draw do
  # GET /about
  get "about", to: "about#index" # get "about" and get "/about" are the same
  # go to the "index" method in about_controller.rb (located in app -> controllers)
end
```
- the default HTML wrapper layout comes from the **'app -> views -> layouts -> application.html.erb'**
```HTML
<!--application.html.erb-->
<!DOCTYPE html>
<html>
  <head>
    <title>ScheduledTweets</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %> <!--this is Ruby Scripts-->
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
    <!--loads CSS from Rails App-->
  </head>

  <body>
    <%= yield %> <!--this will be replaced by the content that we write/render-->
  </body>
</html>
```

# **Root Route**
```ruby
Rails.application.routes.draw do
  # GET /about
  get "about", to: "about#index"

  # setting the ROOT route, the following syntax all have the same meaning
  get "/", to: "main#index"
  get "", to: "main#index"
  root to "main#index"
end
```

# **Partials Rendering**
```HTML
<!--application.html.erb-->
<!DOCTYPE html>
<html>
  <head>
    <title>ScheduledTweets</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>

  </head>

  <body>
    <%= render partial: "shared/navbar"%>
    <!--partial here means it's not a full template, only rendering a portion of the page-->
    <!--it will look into "app->views->shared-" with filename "_navbar.html.erb"-->
    <!--here the navbar is set accross the webpage-->

    <div class="container">
        <!--wrap the content in a container and prevent it from pushing it to the edge-->
        <%= yield %>
    </div>
  </body>
</html>
```
- **"_partial.html.bar"** the underscore at the front means it's a partial rendering, and it seperates from regular template (obly meant for partial rendering)
  
# **URL Helpers and link_to**
- Ruby provides a helper called **link_to**
- We can check the routes available by typing the following command:
```cmd
rails routes
```
- **Prefix** is the name of the route that allow us to reference in Ruby code
```HTML
<!--_navbar.html.erb // PARTIAL RENDERING FILE-->
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <%= link_to "Navbar", root_path, class:"nav-link" %>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <%= link_to "Home", root_path, class:"nav-link" %>
        </li>
        <li class="nav-item">
          <%= link_to "About", about_path, class:"nav-link" %>
          <!--the parameter after "link_to" is the name to be displayed-->
          <!--the 2nd parameter is "route name" + "_" + "path / url"-->
        </li>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

# **Flash Messages**
- **Flash** is inherited from application controller
```ruby
class MainController < ApplicationController

    def index
        flash[:notice] = "Logged in successfully" # these flash messages persist in cookie for one more additional request
        flash[:alert] = "Invalid email or password"
        # flash[:notice].now = "Logged in successfully"  ## use ".now" to display only on the current request
        # flash[:alert].now = "Invalid email or password"
    end

end
```

```html
<!--_flash.html.erb--> 

<%if flash[:notice]%> <!-- here we dont use "%=" because we dont want it print out the return value in html-->
  <div class="alert alert-info mt-4" role="alert">
      <%= flash[:notice]%>
  </div>
<%end%>

<% if flash[:alert]>
  <div class="alert alert-warning mt-4" role="alert">
      <%= flash[:alert]%>
  </div>
<%end>
```

# **Creating User Model**
- **Model** is like a database table in Rails App
- **Migration** allow us to add new field into an database table without modifying the existing content, eg: "User" table has 2 field (email,password), we can add a new field called "name" without affecting the existing datas in the table
``` ruby
rails generate model User email:string password_digest_string
# This command is used to generate a model
# "User" is the model name, there are 2 column: email(string) and password(string)

      invoke  active_record
      create    db/migrate/20220226091700_create_users.rb # this is the database migration file, it defines the new table and changes to it
      create    app/models/user.rb
      invoke    test_unit
      create      test/models/user_test.rb
      create      test/fixtures/users.yml

rails db:migrate
# to create the database table
```
- We can interact with the tables in terminal using the **Rails C (Rails Console)**, might need to uncomment bkrypt in Gemfile and run bundle to install the library
```ruby
User.all    # get all records in the "User" table\
User.first  # get the first record in the "User" table
User.last   # get the last record in the "User" table 

# example on how to add a user into the database
User.create({email:"zhinsheng97@gmail,com",password:"password",password_confirmation:"password"})
# this will create a record with the above information in the "User" table
```
## **Attributes validation**
- we have to verify the attributes of a record before saving it to the database, eg: email cannot be blank
1. we can add the **validates: email,presence: true** in user.rb
2. we can go to the migration file and add **t.string:email,null: false**
```ruby
# user.rb

class User < ApplicationRecord # we can use this file to query the database
    has_secure_password 
    # add password confirmation for the password_digest field, password confirmation is a virtual attribute that wont get saved into the database
    # it will ensure password and password_confirmation matched, and run the "bcrypt" to hash the password to create the digest

    validates: email,presence:true # check and make sure the email attribute is there before saving it to the database
end
```
```ruby
# migration file
class CreateUsers < ActiveRecord::Migration[7.0]
  def change
    create_table :users do |t|
      t.string :email, null:false # make sure the email attribute cannot be NULL
      t.string :password_digest

      t.timestamps
    end
  end
end
```
```ruby
rails db:rollback     # use rollback to undo the migration and add on any new changes or features
rails db:migrate
rails db:migrate:redo # rollback + migrate
reload!               # reload the database with any new changes after saving the ruby codes
```
# **Creating a sign-up form**
- the same URL can handle multiple types of request (**GET, POST, PATCH, PUT, DELETE**)

```html
<h1> Sign Up </h1>

<h1> Sign Up </h1>

<%= form_with model: @user, url: sign_up_path do |form|%>
    <div class="mb-3">
        <%= form.label :email %>
        <%= form.text_field :email, class: "form-control", placeholder: "steve@apple.com" %>
    </div>
    <div class="mb-3">
        <%= form.label :password %>
        <%= form.password_field :password, class: "form-control", placeholder: "password" %>
    </div>
    <div class="mb-3">
        <%= form.label :password_confirmation %>
        <%= form.password_field :password_confirmation, class: "form-control", placeholder: "password" %>
    </div>

    <div>
        <%= form.submit "Get Started" , class: "btn btn-primary" %> 
        <!-- the default tag is smart enough to look at the form name, and display the text "Create" + form name, in this case "Create Form" -->
        <!-- in this case we overwrite the display content with the text "Get Started" -->
    </div>
<% end %>
```
```ruby
# routes.rb
Rails.application.routes.draw do

  get "about", to: "about#index"

  get "sign-up", to: "registrations#new"
  post "sign-up", to: "registrations#create"

  root to: "main#index"

end
```
# **Handling Sign Up Forms**
- We use **params** to retrieve all the parameters returned when user make a POST request
- **params** can come from the routes, or URLs (extract parameters from the URL itself)
```ruby
# example: these are the parameters when a user submit the form and make a POST request
Parameters: {"authenticity_token"=>"[FILTERED]", "user"=>{"email"=>"zhinsheng97@gmail.com", "password"=>"[FILTERED]", "password_confirmation"=>"[FILTERED]"}, "commit"=>"Sign Up"}
```
# **Login with Session Cookies**
- Rails provide 2 cookies: **Session Cookies, Sign Cookies**
- **Session Cookies** is encrypted, no one can tamper and modify (even browser)

# **Rails Mailer**
- We can generate a **Mailer** to send emails to end-users
- **Mailers** work very similar to **Controller**, except mailer is generating HTML and text in other format
```ruby
rails g mailer Password reset
# rails g mailer -> ask Rails to generate a mailer
# "Password" is the mailer name
# "reset" is the mail template that the mailer should use
```
- Rails is able to generate a token to user for password reset (random, unique so it can identify which user is resetting the password), and can also have expiration to reset password
```ruby
# go to "rails c" (rails console)
user.signed_id
user.signed_id(expires_in:15.minutes) # generate a unique token for a particular user that will expire in 15 mins
user.signed_id(expires_in:15.minutes, purposes: "password_reset") # generate a token that is for "password_reset" purpose
```
- We need to setup a host and default URL option for **Mailer**
```ruby
# add this in config > environments > either development/production/test .rb
# specify the host name
config.action_mailer.default_url_options = {host: "localhost:3000"}
```