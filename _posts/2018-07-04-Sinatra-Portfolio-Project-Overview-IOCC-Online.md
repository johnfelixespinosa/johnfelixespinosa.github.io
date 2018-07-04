---
layout: post
title: "Sinatra Portfolio Project Overview - IOCC Online"
date:  2018-07-04 14:30:35
categories: code
---

![Scraper Assessment](/img/IOCConline.png)

This project has proven to me the one thing my programmer friends have repeated over and over. The best way to learn is to simply build something. Build something of your own, from scratch, stumble through it, get really really excited at times only to get **really really** frustrated at other times, finally, pat yourself on the back when you've overcome the frustrations, and you have something close to what you invisioned. 

IOCC online was a rollercoaster of a project for me. Initially I just wanted to create an application that allowed for students to simply CRUD class schedules. Initially they would be able to login in to the app, then fillout a schedule. Soon I realized, well this is dumb, why not see if I can have a second user type such as instructors, who create the courses for the students to signup for. And thats when things got out of hand. I realized, well ok... so now I'm going to need another model...right? Shoot, now I'm going to have to deal with more associations, this is going to get confusing. **Note:** *after writing out that last sentence I now realize, well it wasn't really that confusing, but at the time it set my brain into overdrive, and I quickly became overwhelmed, so yes, at the time it was confusing!*

Well, I got lazy, and I decided I didn't really feel like going back to my editor and creating a new model, having to do migrations and all that. So I wanted to see if there were any other ways of doing so, such as just having a class attribute that dictated a usertype. Google and stackoverflow was my friend and I came across this stack question. [Multiple Types of Users on RoR](https://stackoverflow.com/questions/24479839/multiple-types-of-users-on-ruby-on-rails) 

```ruby
class AddRoleToUsers < ActiveRecord::Migration
  def change
    add_column :users, :role, :integer
  end
end
```

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