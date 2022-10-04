---
title: Create a website on Github using Jekyll
date: 2022-10-02 14:06:30 -0100
categories: [Wesbite]
tags: [tutorial]     # TAG names should always be lowercase---
img_path: /commons/images
#image:
   #path: /chirpy.jpeg
   #width: 300   # in pixels
   #height: 300   # in pixels
---

# Create a website like this one on Github using Jekyll!
As this website is fairly new, it would be appropriate to share how I created this website using readily available and free services.

![](/chirpy.jpeg)

## Quick Start
Firstly, [Jekyll Docs](https://jekyllrb.com/docs/installation/) provides instructions to install `Ruby`, `RubyGems`, `Jekyll`, and `Bundler`.  You will also need to install [Git](https://git-scm.com/)

### Step 1 - Find a theme
There are many different paid and free themes available. I recommend spending some thought towards what you would like to achieve with your own website and in addition what you will require of the website to best assist in what would are trying to achieve. 

Some themes can be found at for example:
-   [GitHub.com #jekyll-theme repos](https://github.com/topics/jekyll-theme)
-    [jamstackthemes.dev](https://jamstackthemes.dev/ssg/jekyll/)
-    [jekyllthemes.org](http://jekyllthemes.org/)
-    [jekyllthemes.io](https://jekyllthemes.io/)

The theme that I have chosen and quite like is the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) theme. 

Create a new repository from the template you choose and name it `<GH_USERNAME>.github.io`, where `GH_USERNAME` represents your GitHub username.

### Step 2 - Pull the Repository to your Computer
I use and enjoy [Visual Studio Code](https://visualstudio.microsoft.com/) as a code editor which offers compatibility with Github. This means, any changes made to your website locally can be pushed to Github.
All you need to do is connect Visual Studio Code to your Github account and pull your repository.

### Step 3 - Install Dependencies
Before running for the first time, go to the root directory of your site, and install dependencies as follows:
```
$ bundle
```

### Step 4 - Running Local Server
Run the following command in the root directory of the site:
```
bundle exec jekyll s
```

This will provide a local version of your website which can be viewed at [http://localhost:4000/](http://localhost:4000/). Any changes made to your website will be presented after a simple refresh (except for changes made to the \_config.yml file which will require you to run the above code again) 

### Troubleshooting
#### require: cannot load such file -- webrick
I came across this issue which can be resolved by adding webrick.
Dealing with: `require': **cannot load such file -- webrick**
```
bundle add webrick ui

