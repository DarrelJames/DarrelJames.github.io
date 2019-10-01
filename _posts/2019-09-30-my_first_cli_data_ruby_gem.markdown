---
layout: post
title:      "My first CLI Data ruby gem"
date:       2019-09-30 21:07:15 -0400
permalink:  my_first_cli_data_ruby_gem
---


Whenever my girlfriend travels, she likes to visit the local museums. So I decided to create a gem that would scrape a website with a list of museums. I did a quick google search and found this website, [Smithsonian](https://www.smithsonianmag.com/museumday/museum-day-2019/). They hold an annual event called Museum Day, which happened two weeks ago.

Going through that website
1. You can search museums by zip code
2. Upon entering a zip code, it lists museums in the area
3. Choosing a museum will then give you more detailed information.

#### I decided to name my CLI gem: museum_day


With that, I had enough information to get my project started.

I started off by running

> bundle gem museum_day

This command generated a project skeleton for creating a rubygem

![](https://i.imgur.com/b5XloIv.png)

I created a few more files

**/bin/museum_day**<br>
**/lib/museum_day/scraper.rb**<br>
**/lib/museum_day/museum.rb**<br>
**/lib/museum_day/cli.rb**

#### /bin/museum_day

```
#!/usr/bin/env ruby

require "bundler/setup"
require "museum_day"

MuseumDay::CLI.new.call
```

This is our executable. It allows a user to run my gem by just typing `museum_day`.
It creates a new instance of CLI and calls the method `#call`.

#### scraper.rb

The purpose of this file to scrape all the museums based on the zipcord the user enters.
Contains 3 methods.

1. **get_museums_page**

uses Nokogiri to parse the HTML and return it.

2. **scrape_museums_index**

calls #get_museums_page and retrieves information using css selectors

3. **make_museums**

interates through #scrape_museums_index and call a class method from Museum to instantiate new objects

```
class MuseumDay::Scraper

  attr_accessor :zipcode

  def initialize(zipcode)
    @zipcode = zipcode
  end

  def get_museums_page
    Nokogiri::HTML(open("https://www.smithsonianmag.com/museumday/search/?q=&around_zip=#{zipcode}"))
  end

  def scrape_museums_index
    self.get_museums_page.css("div.museum div.museum-text")
  end

  def make_museums
    scrape_museums_index.each do |museum|
      MuseumDay::Museum.new_from_index(museum)
    end
  end

end
```

#### museum.rb

The purpose of this file is to keep track of all the museum objects that's been instantiated and set different attributes including the :address, :phone_number, :website_url, :fb, :twitter, and finally the :description.

```
class MuseumDay::Museum

  attr_accessor :name, :city, :url, :address, :phone_number, :website_url, :twitter, :fb,
  :description, :hours, :doc

  @@all = []

  def self.new_from_index(museum)
    self.new(
      museum.css("h4.name").text,
      museum.css("h5.location").text,
      museum.css("a").attribute("href").value,
      museum.at("div strong").next_sibling.text.strip
    )
  end

  def initialize(name = nil, city = nil, url = nil, hours = nil)
    @name = name
    @city = city
    @url = url
    @hours = hours
    @@all << self
  end

  def self.all
    @@all
  end

  def self.find(id)
    self.all[id-1]
  end

  def address
    @address ||= doc.css("p.address").text.strip
  end

  def phone_number
    @phone_number ||= doc.at("i.fa-phone").next_sibling.text.strip
  end

  def website_url
    @website_url ||= doc.css("i.fa-external-link + a").attribute("href").value
  end

  def social_urls
    social_links = doc.css("div.contact a").collect { |link| link.attribute("href").value }

    social_links.each do |link|
      if link.include?("twitter")
        self.twitter = link
      elsif link.include?("facebook")
        self.fb = link
      end
    end
  end

  def description
    @description ||= doc.css("div.aux-info p").first.text
  end

  def doc
    @doc ||= Nokogiri::HTML(open("https://www.smithsonianmag.com#{self.url}"))
  end

  def self.clear_all
    @@all.clear
  end
end
```

#### CLI.rb

Finally, the file that brings everything together.
I spent most of my time working in this file.

This file is responsible for displaying information based on the user's input.

Check out my repo for the full source code [here](https://github.com/DarrelJames/museum_day).


#### Try it your self!

You can install by typing

`gem install museum_day`

and then running it by typing

`museum_day`

