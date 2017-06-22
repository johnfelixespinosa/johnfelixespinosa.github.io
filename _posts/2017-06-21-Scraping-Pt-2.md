---
layout: post
title: "Scraping Pt. 2"
date:  2017-06-21 11:12:35
categories: code
---

![Scraper Assessment](/img/CodeReviewSS.png)

The scraping project from my previous post ended up being a success, in addition, I got to experience my first code review with one of the team members from Learn. Prior to the review I was hesistant, half expecting the reviewer to rip my code to shreds, but in actuality it was a wonderful experience. Cernan, my reviewer, gave me pointers such as which methods should be handled by which classes. For example, the following class method **new_from_index_page(p)**, I had within my Posts class. However, it shouldn't be the Post class's job to deal with any CSS or tags. It made much more sense to move this method to the Scraper class, and so that's what I ended up coding during the review with Cernan. 

```ruby
class LearnBlogCLI::Posts
 
   attr_accessor :name, :url, :author, :description 
  
    @@all = []
  
   def self.new_from_index_page(p)
     self.new(
       p.css("h2").text,
       p.css('.post-img').css("a").attribute("href").text,
       p.css('.post-footer').css("a").text,
       p.css('.post-txt').css("p").text
       )
   end
```

```ruby
class LearnBlogCLI::Scraper

   attr_accessor :doc
 
    @doc = ""

  def new_from_index_page(p)
     LearnBlogCLI::Posts.new(
       p.css("h2").text,
       p.css('.post-img').css("a").attribute("href").text,
       p.css('.post-footer').css("a").text,
       p.css('.post-txt').css("p").text
       )
   end
```

All in all, the code review was refreshing and helped me out tremendously. Being able to explain my code fully, while also having lightbulbs going off on how to improve it was invaluable. Thanks alot Cernan!

### Scraper Project #2

After completing my student scraping project and passing my code review and assessment I decided to build out yet another scraper project, not only for the practice, but to challenge myself. I settled on the idea of building a CLI that scrapes the top must have vinyl records for anyones collection. 

![Top Vinyls](/img/TopVinylsSS.png)

I want this scraper to provide more data to the user, and it gets a bit more complicated, as it will require me to scrape from multiple pages. It's a work in progress, but so far moving along nicely. I should have it complete by the end of the week. Ultimately, I'd like to be able to provide the user with an album track listing, and possibly info on pressings and release dates. 

#### _-John Espinosa_  