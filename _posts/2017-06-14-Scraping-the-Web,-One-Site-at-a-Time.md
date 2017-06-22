---
layout: post
title: "Scraping the Web, One Site at a Time"
date:  2017-06-14 02:44:35
categories: code
---

![Scraping](/img/ScraperSS.png)

Well that's it! After weeks of on and off again work, I've finished my scraping project, the final project for the Object Oriented Ruby section of my Learn program. It may seem lackluster and simple, but it was so much fun finishing up, and I'm pretty proud of it. 

### Takeaways

+ **CSS** is daunting at first. Using tags and selectors, finding the data your after, navigating and inspecting page source code and piecing it all together is not easy at first. I'm sure with more experience and learning more tools and shortcuts will make it manageable.  
+ **Nokogiri** is pretty cool, and I want to immediately build another scraper because of it.
+ **Pry** is even cooler! I started using it a lot more while building this scraper, and man, it really helped me understand what my methods were doing, and how my objects were misbehaving, lol. 

### Learn Blog CLI Scraper

So what exactly does this project do, you may ask. 
The application scrapes the [Learn.co Blog](http://blog.flatironschool.com) and generates data from each post. The user first chooses a category for which they would like to see all the current posts, from that selection, all the current posts in that category are pulled up for the user to see. Lastly the user can choose a post they would like more info about, this generates the data for that post in the following format

- post title
- post author
- post description
- post url 

Amazing! Right? 

I chose to scrape the blog initially because, while inspecting the page, the selectors were simple enough for me to follow, and the data I wanted was right there. Granted, I was also fresh out of ideas for any other sites or data to build a project around. When building out the scraper I used two prior student built scrapers as a guide to help me along. They were [Now Playing](https://github.com/learn-co-curriculum/now-playing-cli-gem) and the [Worlds Best Restaurants](https://github.com/dannyd4315/worlds-best-restaurants-cli-gem) gems. I spent a day or two just familiarizing myself with the code for both these gems and following along to understand what each class was doing and what jobs they were assigned. Using these two as guides, I built out my main three classes which were the CLI class, Post class, and scraper class. 

#### Scraper Class

The scraper class job was to use the gems open-uri and nokogiri to access the correct url for the specific blog post category the user inputed. Once accessing the correct url, it would enumerate through that pages css finding the individual posts, thus creating new post class objects. Rinse and repeat for everytime the user decides to call upon a new blog post category. 

#### Post Class

The post class stored each individual post into a class array. Using css selectors, it would make new posts, each with four attributes or variables, the post title, author, description, and url. The post class also had the methods to list all the posts names, as well as show all the data for any individual post. 

#### CLI class

Naturally the CLI class is the class that gets called upon when the application is first run. It guides the user through the app and what it does. It takes in user input to tell the scraper class which page url to scrape, which inturn allows the post class to populate its array with the post objects that contain their individual attributes. Lastly the CLI class had the methods that called upon the post class methods that printed the user requested data onto the screen. 

Once I was able to wrap my head around what I wanted each class to do, building out the CLI from the top down and working through it became simpler. Having the scraper class deal with just the url of the specific page, allowed me to focus on the post class and finding the right selectors for the data I wanted there. The CLI class required some sprucing up as far as interface and user readability, but that wasn't technical. 

### Future refactoring 

I can go through the entire application and can refactor a lot of my redundant code such as my print_category method in the CLI class along with the make_posts method within the scraper class. I know I can find a more elegant way to do what those methods intend to do rather than repetitive else/if statements. I also plan to re-examine my gets user input sections within the CLI, as I don't believe my begin/rescue features are working properly. 

As it is currently, the class variable @all within the post class stores the posts for only one category at a time. If the user decides they would like to see the posts of a different category, then the @all variable is cleared using the clear class method. This works, but what if I wanted to add later on find by name or a search by author feature? The app wouldn't be able to do so as it only stores the info for one category at a time. What if an author has a post in two separate categories? The application wouldn't be able to do that function. I'm still mulling over how I would store the posts objects, I'm sure the solution is simple and I'm just over complicating it mentally. 

### Conclusion

Being able to pull data from a site of my choosing seems so powerful. As big as the web is, I'm sure there are literally an endless amount of gems that could be built that would be so useful to a lot of people. What about a site that scrapes the current used bin selection of vinyl LPs from a local record shop, and spits out the populated list in alphabetical order? If there is a vinyl shop that records its current offerings like that, I could totally build that. I could expand on that and have that populated list cross referenced into Amazon or something and see what that vinyl goes for new or used, and even give the user a thumbs up or down whether or not the price listing at the local vinyl shop is a deal or a ripoff. Heck, if I wanted to, I could take the title of each vinyl, and then find a site to scrape the track listing for that vinyl, and generate that data for the user as well. So many possibilities! I'm getting ahead of myself now, but man, wow!

#### _-John Espinosa_  