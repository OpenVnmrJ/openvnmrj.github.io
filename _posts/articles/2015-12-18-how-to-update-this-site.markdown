---
layout: article
title: How to Update This Site
date: 2015-12-18T19:53:48-05:00
author: tim_burrow
published: true
modified:
categories: article
excerpt:
tags: []
image:
  feature:
  teaser: 400x250.gif
  thumb: 
---

## How to contribute this website

We welcome anyone to contribute to this website. The easiest way is to simply file an issue in the [issue tracker](https://github.com/OpenVnmrJ/openvnmrj.github.io/issues).

If you are want to fork this website and issue a pull request, you may do so too. Again, first file an issue describing the bug or feature or article you want to add. Also mention you'll be working on it, so we won't duplicate your work.

You'll need to sign a Contributor License Agreement too. When you make a pull request the CLA assistant will prompt you.

## Submitting an update

1. Start by forking this repository [openvnmrj.github.io](https://github.com/OpenVnmrJ/openvnmrj.github.io) on GitHub. 
2. Make a new branch; please keep your changes small and atomic in your branch. It's easier for us to merge your pull-request later.
3. Check that your chnages render OK offline. You'lll need to set up a Jekyll install with ruby, see below on how to do this.
4. Do you best to have a [well-formed commit message](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) for each change.
5. Push your changes to your repository and submit a pull-request.

## Setting up a local Jekyll environment on Linux (Ubuntu Trusty Tahr)

This walkthrough is for Ubuntu 14.04 Trusty Tahr. For CentOS or RHEL, use `yum install` in place of `apt-get install` 
See at the end for tips for OS X.

### Git

First , install git and a few extra libraries. Ubuntu Trusty has an old version of git and I like to replace it

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install -y git libssl-dev libreadline-dev zlib1g-dev nodejs
```

### Ruby and Bundler

Next, install RBEnv, bundler and ruby 2.2.3; see [https://github.com/rbenv/rbenv](https://github.com/rbenv/rbenv). This makes sure you are using the correct gems and ruby version. For example, GitHub uses Jekyll 2.4.0, not the latest version.  

```bash
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
rbenv install 2.2.3
rbenv rehash
rbenv local 2.2.3
gem install bundler
```

###  Github
Add a SSH key to your github account; make a negit push --set-upstream origin article-how-to-update-websitew key using keygen if you don't have a public key.

```bash
ssh-keygen
cat ~/.ssh/id_rsa.pub
```
paste into Profile>SSH keys.git push --set-upstream origin article-how-to-update-website

Clone the website repository, replacing "timburrow" with your own GitHub username:  

```bash
git clone --recursive git@github.com:timburrow/openvnmrj.github.io.git

```  
(use --recursive to pull in the git submodule of documentation)  
Add upstream to the "live" website; we'll only pull down to make sure the local website is up-to-date.

```bash
git remote add upstream https://github.com/OpenVnmrJ/openvnmrj.github.io.git  
git remote -v  
git checkout master  
git fetch upstream master -v  
git merge upstream/master  
```

Also, if you  haven't use git before, set your username and email. Use the same email you use for GitHub.

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

#### Documentation

The repository at https://github.com/OpenVnmrJ/Documentation.git is pulled in as a submodule into _documentation. Avoid making changes in _documentation. Changes will be lost when you update the Documentation repository. 

To update the submodule, at the top of the main git repository (that is, not inside _documentation)  

```bash
git submodule update --remote
```

### Install gems

Gems are Ruby programs and libraries. To maintain compatibility with GitHub pages, only use the gems and gem versions specified in the repository. Using RBEnv and Bundler makes this easy for you.  

```bash
cd openvnmrj.github.io/
bundle install
bundle update
```

### Test your local copy

Start up Jekyll to see your local copy. Use the development configuration which uses the local host for URLs.  

```bash
bundle exec jekyll serve --config _config-development.yml --detach
```

If you connect to [http://127.0.0.7:4000/](http://127.0.0.7:4000/) the local website should appear in your browser.  

### Jekyll

For more information of Jekyll and Skinny-Bones, see:  

- [http://jekyllbootstrap.com/lessons/jekyll-introduction.html](http://jekyllbootstrap.com/lessons/jekyll-introduction.html)  
- [https://mmistakes.github.io/skinny-bones-jekyll/getting-started/](https://mmistakes.github.io/skinny-bones-jekyll/getting-started/)  

Here is a summary of the folders:

- _config.yml: Stores configuration data.
- _includes: This folder is for partial views
- _layouts: This folder is fand make sure the lor the main templates your content will be inserted into. You can have different layouts for different pages or page sections.
- _posts: This folder contains your dynamic content/posts. the naming format is required to be @YEAR-MONTH-DATE-title.MARKUP@.
- _site: This is where the generated site will be placed once Jekyll is done transforming it. GitHub generates this, so don't put it into the repository
- index.md (or html)
- images: Folder of imagesDo not put _sites in the repository; GitHub will run Jekyll and create the sites. 


### Octopress

Articles can be created using Octopress to make the page template. Dynamic content, such as articles or posts will show up on the front page automatically. Use folders to group content within the _posts folder. Only those in "news" will show up on the news page.  

```
_posts/  
  articles  
  news  
  posts  
```
The following is a quick way to add a new article. We make sure we are up-to-date with the "live" site, then make a new branch.  

```bash
git checkout master  
git fetch upstream master -v  
git merge upstream/master
```  

Next we make a new branch and add our article, replacing "New article" with the actual article title. There are templates for articles, media, pages, and posts in the `_templates` folder. Your article will be made in `_posts/articles` as specified in the `--dir article` directive. 

```bash
git checkout -b new-article
bundle exec octopress new post --dir articles --template article "New article"
```

If you want to put your name and picture in the article, edit `_data/authors.yml`. Pictures go in the `images` folder.

Now edit the file created. For Jekyll, the filename like `YYYY-mm-dd-new-article.markdown`. A header section of YAML is made that looks like:  

```YAML
layout: article  
title: How to Update This Site  
date: 2015-12-18T19:53:48-05:00  
author: tim_burrow  
published: true   
modified:  
categories: article   
excerpt:  
tags: []  
image:  
  feature:  
  teaser: 400x250.gif  
  thumb:  
```

Add a "feature" image that appears at the top of the web page and a "teaser" image.

### Markdown

Following the YAML section, write your article using [Markdown](https://help.github.com/articles/markdown-basics/).  
I use [Brackets](https://github.com/adobe/brackets/releases) in Ubuntu and [OS X](http://brackets.io/) for writing Markdown, but any text editor will do.

Use `{% raw  %}{{site.baseurl}}{% endraw  %}` in place of `https://openvnmrj.org/` so URLs will work in development. For example, the image below if made from  

```
![Splash image]({% raw  %}{{site.baseurl}}{% endraw  %}/images/400x250.gif)
```

![Splash image]({{site.baseurl}}/images/400x250.gif)

### Publishing

After you have done your article, and it looks OK in development, you are ready to commit it and push it to GitHub and make a pull request. Congratulations!

```bash
git add _posts/YYYY-mm-dd-new-article.markdown
git commit -m "Added New article"and nece-
git push --set-upstream origin new-article
git push origin
```

You'll need to push your branch to GitHub too, otherwise git will throw and error and tell your what to do using the line `git push --set-upstream origin new-article` where new-article is your branch name.
Now, your spiffy new article is on GitHub, but in your repository and in your branch. So now ask for a [pull request](https://help.github.com/articles/using-pull-requests/). Don't forget to switch to your branch in GitHub before making the pull request

## Tips for OS X

### Install Xcode

For OS X, install Xcode and the command line tools. In the terminal type:

```bash
sudo xcode-select --install
```

This installs git along with the compilers and headers necessary to install gems with native code.  

### Install Ruby and Nokogiri

Install RBEnv and Bundler

```bash

```

### Ruby and Bundler

Next, install RBEnv, bundler and ruby 2.2.3; see [https://github.com/rbenv/rbenv](https://github.com/rbenv/rbenv). This makes sure you are using the correct gems and ruby version. For example, GitHub uses Jekyll 2.4.0, not the latest version.  

```bash
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
rbenv install 2.2.3
rbenv rehash
rbenv local 2.2.3
gem install bundler
```

###  Github
Add a SSH key to your github account; make a new key using keygen if you don't have a public key.

```bash
ssh-keygen
cat ~/.ssh/id_rsa.pub
```
paste into Profile>SSH keys.

Clone the website repository, replacing "timburrow" with your own GitHub username:  

```bash
git clone --recursive git@github.com:timburrow/openvnmrj.github.io.git

```  
(use --recursive to pull in the git submodule of documentation)  
Add upstream to the "live" website; we'll only pull down to make sure the local website is up-to-date.

```bash
git remote add upstream https://github.com/OpenVnmrJ/openvnmrj.github.io.git  
git remote -v  
git checkout master  
git fetch upstream master -v  
git merge upstream/master  
```

Also, if you  haven't use git before, set your username and email. Use the same email you use for GitHub.

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

#### Documentation

The repository at https://github.com/OpenVnmrJ/Documentation.git is pulled in as a submodule into _documentation. Avoid making changes in _documentation. Changes will be lost when you update the Documentation repository. 

To update the submodule, at the top of the main git repository (that is, not inside _documentation)  

```bash
git submodule update --remote
```

### Install gems

Gems are Ruby programs and libraries. To maintain compatibility with GitHub pages, only use the gems and gem versions specified in the repository. Using RBEnv and Bundler makes this easy for you. However, Nokogiri does not install easily. Use the following, changing the sdk depending on your system, here, on El Capitan, the SDK is MaxOS10.11.  

```bash
cd openvnmrj.github.io/
gem install nokogiri -v ‘1.6.7' --\
--with-xml2-include=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/usr/include/libxml2/ \
--with-iconv-include=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/usr/include/ \
--with-iconv-lib=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/usr/lib --use-system-libraries \
--with-xml2-lib=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/usr/lib
bundle install
bundle update
```

### Test your local copy

Start up Jekyll to see your local copy. Use the development configuration which uses the local host for URLs.  

```bash
bundle exec jekyll serve --config _config-development.yml --detach
```

If you connect to [http://127.0.0.7:4000/](http://127.0.0.7:4000/) the local website should appear in your browser.   

### Jekyll

For more information of Jekyll and Skinny-Bones, see:  

- [http://jekyllbootstrap.com/lessons/jekyll-introduction.html](http://jekyllbootstrap.com/lessons/jekyll-introduction.html)  
- [https://mmistakes.github.io/skinny-bones-jekyll/getting-started/](https://mmistakes.github.io/skinny-bones-jekyll/getting-started/)  

Here is a summary of the folders:

- _config.yml: Stores configuration data.
- _includes: This folder is for partial views
- _layouts: This folder is fand make sure the lor the main templates your content will be inserted into. You can have different layouts for different pages or page sections.
- _posts: This folder contains your dynamic content/posts. the naming format is required to be @YEAR-MONTH-DATE-title.MARKUP@.
- _site: This is where the generated site will be placed once Jekyll is done transforming it. GitHub generates this, so don't put it into the repository
- index.md (or html)
- images: Folder of imagesDo not put _sites in the repository; GitHub will run Jekyll and create the sites. 


### Octopress

Articles can be created using Octopress to make the page template. Dynamic content, such as articles or posts will show up on the front page automatically. Use folders to group content within the _posts folder. Only those in "news" will show up on the news page.  

```
_posts/  
  articles  
  news  
  posts  
```
The following is a quick way to add a new article. We make sure we are up-to-date with the "live" site, then make a new branch.  

```bash
git checkout master  
git fetch upstream master -v  
git merge upstream/master
```  

Next we make a new branch and add our article, replacing "New article" with the actual article title. There are templates for articles, media, pages, and posts in the `_templates` folder. Your article will be made in `_posts/articles` as specified in the `--dir article` directive. 

```bash
git checkout -b new-article
bundle exec octopress new post --dir articles --template article "New article"
```

If you want to put your name and picture in the article, edit `_data/authors.yml`. Pictures go in the `images` folder.

Now edit the file created. For Jekyll, the filename like `YYYY-mm-dd-new-article.markdown`. A header section of YAML is made that looks like:  

```YAML
layout: article  
title: How to Update This Site  
date: 2015-12-18T19:53:48-05:00  
author: tim_burrow  
published: true   
modified:  
categories: article   
excerpt:  
tags: []  
image:  
  feature:  
  teaser: 400x250.gif  
  thumb:  
```

Add a "feature" image that appears at the top of the web page and a "teaser" image.

### Markdown

Following the YAML section, write your article using [Markdown](https://help.github.com/articles/markdown-basics/).  
I use [Brackets](https://github.com/adobe/brackets/releases) in Ubuntu and [OS X](http://brackets.io/) for writing Markdown, but any text editor will do.

Use `{% raw  %}{{site.baseurl}}{% endraw  %}` in place of `https://openvnmrj.org/` so URLs will work in development. For example, the image below if made from  

```
![Splash image]({% raw  %}{{site.baseurl}}{% endraw  %}/images/400x250.gif)
```

![Splash image]({{site.baseurl}}/images/400x250.gif)

### Publishing

After you have done your article, and it looks OK in development, you are ready to commit it and push it to GitHub and make a pull request. Congratulations!

```bash
git add _posts/YYYY-mm-dd-new-article.markdown
git commit -m "Added New article"and nece-
git push --set-upstream origin new-article
git push origin
```

You'll need to push your branch to GitHub too, otherwise git will throw and error and tell your what to do using the line `git push --set-upstream origin new-article` where new-article is your branch name.
Now, your spiffy new article is on GitHub, but in your repository and in your branch. So now ask for a [pull request](https://help.github.com/articles/using-pull-requests/). Don't forget to switch to your branch in GitHub before making the pull request

## More reading
- http://0a.io/Jekyll-in-3min-for-your-GitHub-page/
- https://help.github.com/articles/using-jekyll-with-pages/
- https://help.github.com/articles/creating-pages-with-the-automatic-generator/
- http://octopress.org/docs/deploying/github/
- http://bundler.io
- https://mmistakes.github.io/skinny-bones-jekyll/getting-started/