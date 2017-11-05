---
layout: post
comments: true
title:  "Adding Comments to a Static Site"
date:   2017-09-17 16:06:22 +0100
categories: web html jekyll disqus static blog
thumbnail: /assets/images/comments.png
---
### Comments
One of the downsides of having a static site is that you cannot add anything that would require any data storage. For a blog, the most notable absense is of any form of comments section. Fortunately there are thrid party providers that can provide comments sections for sites. [Disqus](https://disqus.com) is one such provider that also supports Jekyll.


### Installation
Once you have signed up to Disqus, it walks you through configuring your site with a comments section. For Jekyll the steps are as follows:

For any post that you want to include comments, add a comments variable to the header of the posts YAML file. For this post, for example, it looks like the following:

{% highlight markdown %}
---
layout: post
comments: true
title:  "Adding Comments to a Static Site" ...
{% endhighlight %}

Next we need to add the disqus code to our posts. Disqus will point you towards their [Universal Embed Code](https://disqus.com/admin/install/platforms/universalcode/) page which contains the code to copy. Create a new **disqus.html** page in the **_includes** directory and paste the code in. Uncomment the **disqus_config** section as instructed and configure the variables for your page.  

{% highlight html %}
{% raw %}
var disqus_config = function () {
this.page.url = "http://SITEURL{{ page.url }}";  // Replace SITEURL with your site's main address, page.url will point to his particular post
this.page.identifier = "{{ page.id }}"; 
};
{% endraw %}
{% endhighlight %}

Next go to **_layouts/post.html** and add the following just before the closing artical tag (or wherever you want the comments to appear on your blog posts).

{% highlight html %}
{% raw %}
{% include disqus.html %}
{% endraw %}
{% endhighlight %}

You should now have a Disqus comments section on your post. Run the usual commands to build and deploy Jekyll locally to confirm:

{% highlight shell %}
jekyll build
jekyll serve
{% endhighlight %}

You should now see something similar to the following:
![The Results](/assets/images/comments.png)

### Comment Counts
One additional extra we can add is comment counts to the top of the post. Open **_layouts/default.html** and add the following befote the closing body tag.

{% highlight html %}
<script id="dsq-count-scr" src="//SHORTNAME.disqus.com/count.js" async></script><!--Replace SHORTNAME with your site's disqus shortname-->
{% endhighlight %}

With this script on the site, any url with **#disqus_thread** on the end will automatically get Disqus to count the comments on the page the link points to. So if we go to **_layouts/post.html** and add the following link just above the article body...

{% highlight html %}
{% raw %}
{% if page.comments %}
    <a href="http://SITEURL{{ page.url }}#disqus_thread">0 Comments</a>
{% endif %}
{% endraw %}
{% endhighlight %}

... we should see a comment count at the top of our blog posts:

![Comment Count](/assets/images/comment_count.png)

We can also display this comment count for each post listed on our index page. Open **_layouts/home.html** and add the following inside the *for post in site.posts* loop:

{% highlight html %}
{% raw %}
<a href="http://SITEURL{{ post.url }}#disqus_thread">0 Comments</a>
{% endraw %}
{% endhighlight %}

![More Comment Count](/assets/images/index_comment_count.png)


