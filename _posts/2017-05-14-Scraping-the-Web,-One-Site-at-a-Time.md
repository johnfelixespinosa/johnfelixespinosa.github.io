---
layout: post
title: "Scraping the Web, One Site at a Time"
date:  2017-05-14 02:44:35
categories: code
---

![Scraping](/img/ScraperSS.png)

Well that's it! After weeks of on/off again work, I've finished my scraping project, the final project for the Object Oriented Ruby section of my Learn program. It may seem lackluster and simple, but it was so much fun finishing up, and I'm pretty proud of it. 

### Takeaways

+ **CSS** is daunting at first, HTML, tags, finding the data your after. I'm sure with more experience and learning more tools and shortcuts will alleviate. 
+ **Nokogiri** is pretty cool, and I want to immediately build another scraper that does something cool using it.
+ **Pry** is also pretty cool and amazing! I started using it a lot more while building this scraper, and man, it really helped me understand what my methods were doing, and how my objects were being behaving. 

### Learn Blog CLI Scraper

So what exactly does this project do? You may ask. 
The CLI scrapes the [Learn.co Blog](http://blog.flatironschool.com) and generates data from each post. The user first chooses a category for which they would like to see all the current posts, from that selection, all the current posts in that category are pulled up for the user to see. Lastly the user can choose a post they would like more info about, this generates the data for that post in the following format

+ post title
+ post author
+ post description
+ post url 



#### _-John Espinosa_  