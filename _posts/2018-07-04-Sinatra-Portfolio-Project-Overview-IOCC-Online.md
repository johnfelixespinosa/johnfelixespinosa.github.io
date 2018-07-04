---
layout: post
title: "Sinatra Portfolio Project Overview - IOCC Online"
date:  2018-07-04 14:30:35
categories: code
---

![Scraper Assessment](/img/IOCConline.png)



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