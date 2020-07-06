---
layout: post
title: "Eloquent Ruby"
date:  2020-07-02 15:30:35
categories: code
---
Concepts and tidbits from Eloquent Ruby by Russ Olsen that reinforced, taught me something new, or I just found interesting!

## Write Code That Looks Like Ruby

### 1. Parenthesis
Ruby at times tries to minimalize syntax. An example of this, that I was unfamiliar with is in how Rubyists treat parenthesis. The first time I encountered this within a codebase, I was actually confused, as I had not yet begun the practice of omitting parens, and used them at all times.

```ruby
def translate( text, language )
  # Body Omitted
end

translate( "Hello, how are you?", "Spanish" )
```

Without parens

```ruby
def translate text, language
  # Body Omitted
end

translate "Hello, how are you?", "Spanish"
```
The hard and fast rule to this, is usually to INCLUDE the parens, however there are times such as conditions in a control statement where it is best to exclude the parens. Additionally, knowing that this is a practice amongst Rubyists, where sometimes they will be omitted can be helpful when seeing it within a codebase.


```ruby
if ( text.size > 100 )
  puts 'Unable to translate'
end
```
This is better

```ruby
if text.size > 100
  puts 'Unable to translate'
end
```

### 2. Modifiers

Prior to starting my web development career, the bulk of the logic that I would write consisted of verbose, if/else statements. While getting the job done, one of the core fundamentals of writing Ruby is to be concise and write idiomatic code that can be read and understood simply. For example, refactoring the method below, from something I may have written two years ago, to a concise method that I may end up with today.

```ruby
def name=( new_name )
  if not @read_only
    @name = new_name
  end
end
```
This is better
```ruby
def name=( new_name )
  unless @read_only
    @name = new_name
  end
end
```
This is even better
```ruby
@name = new_name unless @read_only
```

### 3. Percent Strings

Another practice I was unfamiliar with was the use of the percent shortcut to turn inelegant code into more readable code. It wasn't until I started looking into codebases that I had not written did I see this practice in the wild.

An array I may have likely written

```ruby
characters = [ 'mario', 'luigi', 'toad', 'bowser', 'yoshi' ]
```
This is much cleaner, easier to read, and convenient
```ruby
characters = %w{ mario luigi toad bowser yoshi }
```

## Symbols
### 1. Symbols stand for something

There can only ever be one instance of any given symbol.
```ruby
me = :player
active_player = me
first_player = :player
```
me, active_player, and first_player all refer to the same object
```ruby
# True!
me == first_player
a.eql?(c)
```
In contrast, if you were to use a string over a symbol, you are making a brand new string object each time.
```ruby
me = "player"
active_player = "player"
```

## Objects
### 1. Most everything is an object

While this concept was not new to me, I found the example to prove this in the book straightforward to drive this concept home.

```ruby
true.class      # Returns TrueClass
nil.class       # Returns NilClass
nil.nil?        # True!!
```
In Ruby, if you can reference it with a variable, it's an object.


#### _-John Espinosa_
