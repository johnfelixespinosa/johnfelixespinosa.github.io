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

## Composing Methods
### 1. Short, coherent methods

This section was interesting to me as it's a practice I'm still actively trying to get better at, and I was reminded of some recent code I wrote, that Rubocop was angry at for being too complex. After sending it off to review, I was left with some code that used defining short methods to lower the complexity, a fundamental and core practice within the Ruby community. The cost of defining a new method is relatively low in Ruby, just an extra def and end. It leads to more elegant code and has the added benefit of making classes easier to test with many fine-grained methods.

Too complex for rubocop
```ruby
def show_status
  if ending_date.present? && ending_date <= Date.current
    "disabled"
  elsif starting_date.nil? || ( starting_date.present? && starting_date.future? )
    "upcoming"
  else
    "enabled"
  end
end
```

Refactored by composing short methods
```ruby
def show_status
  if display_disabled?
    "disabled"
  elsif display_upcoming?
    "upcoming"
  else
    "enabled"
  end
end

def display_disabled?
  ending_date.present? && ending_date <= Date.current
end

def display_upcoming?
  starting_date.nil? || ( starting_date.present? && starting_date.future? )
end
```

It cost me nothing to define methods for the operator expressions, and as a benefit, we've made Rubocop happy, we've made the show_status method much more elegant at first glance to understand, we've defined two methods that clearly state their purpose, as well as have defined methods that can now be tested independently.

### 2. Class Method: Singletons in Plain sight
A singleton is a method defined on an instance of a class. Knowing this, and understanding prior that most things in Ruby are objects that are instances of a Class object. Then it makes sense that Class methods are just singletons.

```ruby
class Document
  class << self
    def find_by_name(name)
      # Method here
    end
  end
end
```

## Blocks
### 1. Block Arguments

Blocks can take arguments, which are supplied as arguments to yield

```ruby
def do_something_with_an_arg
  yield("Hello World") if block_given?
end

do_something_with_an_arg do |message|
  puts "This message is #{message}"
end

// The message is Hello World
```

## Error Handling
### 1. method_missing

You are free to override method_missing in any class and handle the case of missing method yourself

```ruby
class RepeatBackToMe
  def method_missing( method_name, *args )
    puts "Hey, you just called the #{method_name} method"
    puts "With these arguments: #{args.join(' ')}"
    puts "But there ain't no such method!"
  end
end
```

## Monkey Patching
### 1. Alias

alias_method actually copies a method implementation, giving it a new name. It's not that we are redefining the original method, but making a copy of it and naming it something else.

```ruby
class Document

  def word_count
    words.size
  end

  alias_method :number_of_words, :word_count
  alias_method :size_in_words, :word_count
end
```

This results in three methods on a Document instance that will all return the number of words in the document

#### _-John Espinosa_
