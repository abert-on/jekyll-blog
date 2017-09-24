---
layout: post
comments: true
title:  "Building a blog with Jekyll"
date:   2017-08-28 12:01:22 +0100
categories: web html jekyll 
---
## Jekyl
I've wanted to a personal website for a while now. Something for sharing my thoughts and findings beyond my usual day-to-day development work. 

The number of options for doing this seemed a little overwhelming. Go with a big, popular CMS product such as WordPress? Or write something more tailored to my needs using past experiences with Spring Boot and Thymeleaf? Eventually I stumbled across [Jekyll](https://jekyllrb.com). It seemed pretty easy to generate blog-aware pages from it, whilst also allowing a good deal of flexibility. The fact that it generates completely static websites with no database required was a bonus in terms of hosting options. 


## Installation
Being Ruby-based, installation is pretty simple using [RubyGems](https://rubygems.org):

{% highlight shell %}
gem install jekyll bundler
{% endhighlight %}

Next create a new site and Jekyll will create a new directory matching the site name and populate it with all the default content.

{% highlight shell %}
jekyll new sitename
{% endhighlight %}

And that's pretty much it. You can then edit the default content with your own information and add new content that you want on your site. New blog entries can be created as Markdown files in the _posts directory with a naming pattern of YYYY-MM-DD-title.

## Theme
The default Jekyll theme is pretty basic, but fortunately there are a [number](http://jekyllthemes.org) of RubyGem-based alternative themes to choose from. They can be installed by adding the corresponding Ruby Gem to the sites Gemfile and updating the theme section in the sites _config.yml file.

Alternatively you can install the theme gem manually, here are the steps followed to install the [Caymen Blog Theme](https://github.com/lorepirri/cayman-blog) to this site:

1. Intall the theme gem using `gem install jeyll-theme-cayman-blog`
2. Run `bundler info jekyll-theme-cayman-blog` to list the location of the gem
3. copy the contents of the gems folder to the directory of your site. **Note:** This will overwrite any changes you have to the index.md, about.md and contact.md files.
4. Update _config.yml, leaving the `theme` section empty. 
5. Customise the theme assets to your heart's content.

## Deployment
Deploying the site couldn't be simpler. Simply get Jekyll to build the site and all it's static content and then upload the contents of the newly generate _site directory to the root of your hosted website:

{% highlight shell %}
jekyll build
{% endhighlight %}

## Final Thoughts
![The Results](/assets/images/blog.png)

Creating this blog using Jekyll has so far been a very pain free experience. Time will tell whether it will prove flexible enough for my needs, but so far so good.

