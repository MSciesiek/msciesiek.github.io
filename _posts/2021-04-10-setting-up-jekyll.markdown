---
layout: post
title:  "Setting up Jekyll!"
date:   2021-04-10 11:39:59 +0200
categories: jekyll update
---
Jekyll is a very lightweight alternative to i.e. Wordpress that can creates static websites and can be hosted for free on i.e github pages. I decided to give it a try and what you see is the result. The local setup on my linux machine looked like this:

Reinstallation of ruby (optional)
---------------------------------
I had permission issues with ruby (write permissions for /var/lib/gems/...), so I had to reinstall it. I did that based on a [SO solution][so-ruby-reinstall]:

{% highlight bash %}
sudo apt-get remove ruby
cd $HOME
sudo apt-get update
sudo apt install git curl libssl-dev libreadline-dev zlib1g-dev autoconf bison build-essential libyaml-dev libreadline-dev libncurses5-dev libffi-dev libgdbm-dev
curl -sL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash -
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
{% endhighlight %}

Next checked for the available ruby versions with:
{% highlight bash %}
rbenv install -l
{% endhighlight %}

Then I proceded with version 3.0.1:
{% highlight bash %}
rbenv install 3.0.1
rbenv global 3.0.1
{% endhighlight %}


Setting up the bundle for the new site
--------------------------------------

I followed the steps from [jekyllrb] plus added the webrick to the bundle as it's not included by default in ruby 3.x
{% highlight bash %}
cd path/to/dir-with-projects
gem install bundler jekyll
jekyll new site-name
cd site-name
bundle add webrick
bundle exec jekyll serve
{% endhighlight %}
   
Now the page can be accessed locally on http://localhost:4000

More information about Jekyll can be found in [Jekyll docs][jekyll-docs].

[jekyll-docs]: https://jekyllrb.com/docs/home
[so-ruby-reinstall]: https://stackoverflow.com/questions/37720892/you-dont-have-write-permissions-for-the-var-lib-gems-2-3-0-directory
[jekyllrb]: https://jekyllrb.com/
