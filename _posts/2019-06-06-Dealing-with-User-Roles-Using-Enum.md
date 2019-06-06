---
layout: post
title: "Dealing with User Roles Using Enum"
date:  2019-06-06 15:13:35
categories: code
---

One of the most common features to be implemented in a web application is the ability to specify roles. Much like the last time I implemented a roles feature [(here)](https://github.com/johnfelixespinosa/React-Practice/tree/master/instagram-mock), it took me longer than it should have. Going in one direction, only to switch gears to another, ultimately coming full circle back in the original direction. To review the concept, I'd like to identify the pros and cons of the implementation method I chose.

The task at hand for this implementation was as follows 

- Users have first names and last names

- Groups have a name

- Users can attend multiple groups and have roles in each group (Organizer, Presenter, and Participant)

And, that's it. Atleast for the requirements needed for the roles implementation. In order to accomplish this I decided to implement the Rails enum technique. Here is an example of the technique in a User model. 

```ruby
class User < ActiveRecord::Base
  enum role: [:user, :vip, :admin]
  after_initialize :set_default_role, :if => :new_record?

  def set_default_role
    self.role ||= :user
  end

end
```
The application uses the *enum* method to assign roles to instances of user, while also providing querying methods such as 
```ruby
user.admin! # sets the role to "admin"
user.admin? # => true
user.role  # => "admin"
```

So using the Rails enum technique for roles can, and it did, work in this application. What I ultimately decided on doing was creating a *has_many through:* association for Users and Groups in the form of an attendance model. Outlined as follows. 
```ruby
class User < ApplicationRecord
  has_many :attendances
  has_many :groups, through: :attendances
end

class Group < ApplicationRecord
  has_many :attendances
  has_many :users, through: :attendances
end

class Attendance < ApplicationRecord
  belongs_to :user
  belongs_to :group

  enum role: [:Participant, :Presenter, :Organizer ]
end
```

A User object and Group object can be persisted normally. In addition, the Attendance object is what associates a users groups and vice versa. When an attendance object is persisted, it also identifies a role. Here is an example.

```ruby
user = User.create(first_name: "John", last_name: "Espinosa")
$<User id: 3, first_name: "John", last_name: "Espinosa">

group = Group.create(name: "Nova Code & Coffee")
$<Group id: 4, name: "Nova Code & Coffee">

attendance = Attendance.create(user_id: user.id, group_id: group.id, role: 1)
$<Attendance id: 12, user_id: 3, group_id: 4, role: 1>
```

Using these associations querying the models can be achieved as follows

```ruby
user.groups ##All groups a user attends
<Group id: 4, name: "Nova Code & Coffee">...

group.users ##All users attending a group
<User id: 3, first_name: "John", last_name: "Espinosa">...

attendance.user ##The attendance object's user
<User id: 3, first_name: "John", last_name: "Espinosa">

attendance.group ##The attendance object's user
<Group id: 4, name: "Nova Code & Coffee">

attendance.role ##The role assigned to this attendance object
"Organizer"
```

In order to query a group object for specific roles, a finder method could be used such as

```ruby
group.attendances.where(role: "Organizer") ##All attendances with Organizer role
<Attendance id: 12, user_id: 3, group_id: 4, role: "Organizer">]
```
The immediate advantage to using this technique is it's simplicity especially for smaller applications. Essentially the technique is equivalent to just adding an attribute column to a table, with the added benefit of avoiding possible errors such as *role = "Orgnzer"*. Enum simply maps values to integers within the database, but still allow querying by name. Another advantage to using enums is the built-in validation we get when assigning a role, for example 

```ruby
class Attendance < ApplicationRecord
  belongs_to :user
  belongs_to :group

  enum role: [:Participant, :Presenter, :Organizer ]
end

attendance = Attendance.create(user_id: user.id, group_id: group.id, role: "Manager")

=> ArgumentError: 'Manager' is not a valid role
```

The biggest disadvantage to using enum is that the integer values are not explicity set. If in the future a new role was to be added, and for whatever reason it was added inbetween to previously set values, such as Manager inbetween Presenter and Organizer, then the enum integer values would remap and the values within the database will no longer be correct. All prior Organizers will now be Managers. We can definitely avoid this however by explicitly setting the values, for example

```ruby
enum role: {
  Participant: 0,
  Presenter: 1,
  Organizer: 2
}
```

This defensively sets up our code base be able to accept any future roles that may be added. 

In conclusion, using enums can be a really useful way for defining roles within an application. It definitely worked for me in this application. By explicitly setting our values, we can guarantee data integrity, while keeping readability, whilst also having built-in validations. 




#### _-John Espinosa_  