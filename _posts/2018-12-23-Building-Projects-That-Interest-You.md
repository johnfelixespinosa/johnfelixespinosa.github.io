---
layout: post
title: "PC Builder - Building Projects That Interest You && Seeing the Web Through the Eyes of a Dev"
date:  2018-12-23 14:30:35
categories: code
---

![PC Builder](/img/pcbuilder.jpg)

As I neared the end of the Rails portion of my curriculum, I had already begun brainstorming on what sort of application to build for my Portfolio project. Like many developers, and I'd wager, not just beginners but devs of all levels, I struggled to come up with anything worthwhile for myself to build, much less any idea that kept my interest level past entering

```ruby
rails new some-app
rails g model user
```

into my console. It was starting to become a real roadblock to me completing the Rails section. One night, burning the midnight oil, indulging in one of my favorite time suck activities, browsing Reddit and Electronic Cyber Deals, I noticed something in my browser that I had never really paid much attention to before, sans working on a dev project of my own. The browsers address bar. I don't know if it was due to dynamic routes and RESTful conventions still being fresh in my mind, or if I was just up way past my bedtime, but the site I was surfing at the time was a site designed to pick out individual parts for a computer build. Each user on the site could create these parts lists and then create pages that shared their computers and setups with the world. I was deep into researching the new graphics cards that were recently released by Nvidia, and talking myself into possibly picking one up during the Cyber Monday deals, when my attention was no longer about the content of the site, but more so the structure of the site. I found myself clicking all the links on the site not interested at all at the pictures or information but simply what was in the address bar, the routing, the mapping, it was a delight to explore a website in a way I had never explored before. I remember having revelations and thinking,    
> "ah ha! that must be a class, and that must be a class, that object belongs to that object, that object has many of those, wow this site is full of all types of classes and objects, but its not complicated at all! I could totally build this!"


```ruby
class User < ActiveRecord::Base
  enum role: [:student, :parent, :teacher, :admin]
  after_initialize :set_default_role, :if => :new_record?

  def set_default_role
    self.role ||= :student
  end

end
```
```ruby
User.roles # => {"student"=>0, "parent"=>1, "teacher"=>2, "admin"=>1} # list all roles
user.student! # make a student user
user.student? # => true # query if the user is a student
user.role # => "student" # find out the user’s role
@users = User.student # obtain an array of all users who are students
user.role = 'foo' # ArgumentError: 'foo' is not a valid, we can’t set invalid roles
```

Woah this was pretty cool! My application was simple enough that using the Enum feature (**Note:** *added to Rails 4.1*) made sense. I simply just wanted to distinguish whether a user was a student or an instructor. After implementing Enum into the app. (**Note:** *in the end I still ended up having to run a new migration*) Things were starting to come together. Until I got to the whole act of enrolling and withdrawing from courses. Which if you think about it was the **MAIN** purpose of my app. Who needs an app that just allows instructors to add courses??!? Who cares? If a student can't even enroll!!? 

Sense of Accomplishment = **1** 
Level of frustration = **10**

### enrollment.rb

My initial approach to this feature was, "Oh! I know, letme just create a new attribute for student users that gets instances of courses for when they enroll!". That'll work right? After working on implementing that for a while, I realized this is a bunch of redundant code, there has got to be a way for me to simply associate a course to a students user_id. That would be much more efficient. That lead me to creating a new model of the concept of Enrollment. When a student decides to enroll, a new Enrollment object is created storing the course_id and user_id. Linking the two. An enrollment has_one user and has_one course! What a revelation. 

```ruby
  get '/courses/:id/enroll' do 
    if logged_in?
      if is_a_student?
          current_course
          @enroll = Enrollment.new(
            :user_id => session[:user_id],
            :course_id => current_course.id
            )
         @enroll.save
         redirect to ("/users/#{current_user.slug}")
      end
    end
  end
```
```ruby
class Enrollment < ActiveRecord::Base
  has_one :user
  has_one :course

end
```

How simple! In the end it still took me a while to write the methods that allowed me to pull out the proper data for courses using the Enrollment objects. But we powered through and the app works as intended. 

Sense of Accomplishment = **100** 
Level of frustration = **mild** 

You can checkout the completed app at [IOCC - Imagine Online Community College](https://github.com/johnfelixespinosa/sinatra_portfolio_project)

#### _-John Espinosa_  