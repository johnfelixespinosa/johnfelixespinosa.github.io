---
layout: post
title: "Eloquent Ruby"
date:  2020-07-02 15:30:35
categories: code
---

### Write Code That Looks Like Ruby

Ruby at times tries to minimalize syntax. An example of this, that I was unfamiliar with is in how Rubyists treat parenthesis. The first time I encountered this within a codebase, I was actually confused, as I had not yet begun the practice of omitting parens when possible.

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






#### _-John Espinosa_
