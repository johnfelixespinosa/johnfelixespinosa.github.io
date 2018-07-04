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

Woah this was pretty cool! My application was simple enough that using the Enum feature (**Note:** *added to Rails 4.1*) made sense. I simply just wanted to distinguish whether a user was a student or an instructor. After implementing Enum into the app. Things were starting to come together. Until I got to the whole ace of enrolling and withdrawing from courses. Which if you think about it was the **MAIN** purpose of my app. Who needs an app that just allows instructors to add courses??!? Who cares? If a student can't even enroll!!? 

Level of satisfaction = 1 
Level of frustration = 10

### Scraper Project #2

After completing my student scraping project and passing my code review and assessment I decided to build out yet another scraper project, not only for the practice, but to challenge myself. I settled on the idea of building a CLI that scrapes the top must have vinyl records for anyones collection. 

![Top Vinyls](/img/TopVinylsSS.png)

I want this scraper to provide more data to the user, and it gets a bit more complicated, as it will require me to scrape from multiple pages. It's a work in progress, but so far moving along nicely. I should have it complete by the end of the week. Ultimately, I'd like to be able to provide the user with an album track listing, and possibly info on pressings and release dates. 

#### _-John Espinosa_  