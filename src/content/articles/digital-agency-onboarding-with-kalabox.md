---
layout: layouts/article.html
title: "How MY AGENCY uses KALABOX to STANDARDIZE and WIN all the LOCAL"
tags: deployment, localdev, strategy, support, testing
permalink: true
author: GNZTRN5K
private: false
mainImage: images/articles/digital-agency-onboarding-with-kalabox/pairodime_x_kalabox.png
img-src: images/articles/digital-agency-onboarding-with-kalabox/pairodime_x_kalabox.png
teaser: Onboarding new team members to your web project can be complicated with even the most integrated DevOps team. Say hello to Kalabox.
date: 2016-09-29
---

![alt text](../../../assets/images/articles/digital-agency-onboarding-with-kalabox/pairodime_x_kalabox.png "PAIRODIME X KALABOX")

## The Woes of Local Web Development

There's a common phrase heard throughout the web development community and feared by all in our office here at [PAIRODIME](http://www.pairodime.com):

> Well...it worked on my machine.

Over the years my team and I have tried to settle on common web development tools that would allow us all to collaborate on digital products and minimize our headaches and redundant speach patterns. Local web development envirnoments were especially difficult to master. Even if we all installed MAMP, XAMP, Virtual Box, or installed native web server stacks, we could not gurantee we were all working under the same development conditions and eventually one of us would wind up with the colloquial WSOD. Maybe it was RAM allocation, maybe it was MySQL tuning for large databases, maybe it was my version of SASS that was not the same as my co-workers. Then there was the dreaded moment of truth when pushing changes to our web hosting service. Or on the flip side of that coin; we download all the website code, assets and database from our web host only to spend the next half a day trying to get our website to load in our local web browser.

After exchanging 'my.conf' and 'php.ini' files over slack (yes - that just happended), we finally find solace. No more WSOD. We can finally begin slaying code like galdiators. All shall rejoice!

Don't celebrate just yet; that was just for one team member. Everybody has their own stack preference, so be prepared to know that you will never be fully prepared to handle every computer setup that hits the sprint conference table.

## Say Hello to Kalabox

[Kalabox](http://www.kalabox.io/) standardizes and optmizes local development for Drupal, WordPress, and web apps. It is easy to install, works on Mac, Windows and Linux. It is easy to use for developers who love GUI apps (looking at you [Devsigners](https://www.devsignercon.com)!), and powerful enough for even the most seasoned command line veterans. It is epsecially awesome when we pair Kalabox with the Pantheon plugin which allows us to create identical clones of our entire Pantheon hosting site environments (including MultiDev environments). Being a Pantheon partner agency this has become especially helpful as we can now use Kalabox to create localized replication of our Nginx, Redis, Varnish, SOLR, PHP, MySQL, terminus CLI and Drush for each Pantheon environment that come built into our web hosting serives.

## Understanding How Kalabox Works

First let me say, I do not claim to be an expert on how Kalabox works. Although Kalabox is open source, I have never forked the repo, commited a patch, or added to the [documentation](http://docs.kalabox.io/) (yet!). I have, however, read all the documentation (at least a couple of times), posted questions on the github issue que, posted replies in the issue queue, posted a message or two on the Pantheon Power User Group thread, and have experimented relentlessly trying to vet Kalabox as a drop in replacement for our team's preferred localized development tool. 

### Kalabox basically works like this:
* Download the Kalabox Application from [GitHub](https://github.com/kalabox/kalabox/releases)
* Install as you would any native app
* Installer creates a virtual machine on your computer using [Virtual Box](https://www.virtualbox.org/) (which comes pre bundled with the application)
* Use Kalabox from the GUI or CLI to create a new app from scratch or pull directly from an exisiting app on Pantheon

![alt text](../../../assets/images/articles/digital-agency-onboarding-with-kalabox/kalabox-pantheon-plugin.png "Kalabox GUI Pantheon Plugin")

* If you pull an app from Pantheon, you have the option of pulling database and files as well as code
* Kalabox uses a series of .yml files in the newly created app to describe the virtualized machine and local computer data sharing as well as other plugins and development tools
* The virtual machine uses [Docker](https://www.docker.com/) for awesome container stacking of things like Redis, MySQL, Drupal, [etc.](https://hub.docker.com/explore/)
* Kalabox (along side virtual Box) creates a shared folder for you to interact with the virtual machine
* On a Mac, the default shared folder is located:

<pre><code class="language-bash">
/Users/yournamehere/.kalabox/apps/
</pre></code>

* You can now edit files in your apps /code/ directory
* Kalabox utilizes [Unison](https://www.cis.upenn.edu/~bcpierce/unison/) in combination with Virtual Box shared file system to synchronize the file changes between the virtual machine and your local machine (at a rate of about 1 second)
* Once your changes are made to your code or files, you can use Kalabox to push your changes to your web host (for us that is Pantheon), this includes database and files!
* Rejoice!

## Reality Check: Create / Push / Pulling Large Apps

We build a lot of sites using Drupal (there I said it). Although we use many technologies to power our digital products we are primarily a Drupal shop. Using Kalabox, I love being able to clone my Pantheon website to my local machine, make some code changes, add new image files and update site config using the Drupal GUI (okay maybe not so much love for Drupal config using admin but you get the idea) and then push all my changes (including database and files) back up to Pantheon in one simple action. This works well for your average brochure website, but many of our brand websites are Drupal Commerce, they have high quality photo assets, fancy-shmancy JavaScripts, extensive contributed and custom modules, and databases that are often over 100mb compressed. Kalabox would be able to push and pull these assets without fail, but the process can seem to take a lifetime (in reality about 20+ minutes or so). 

### Pro Tip

* If you are creating or working on an app with <5 MB Database <70 MB in files => Create, Push and Pull with Kalabox GUI or CLI all day long and enjoy the simple freedom of deploying your app with ease.
* Your site will be created in less than 5 minutes and push to the web in less than 5 minutes.
* Many of our fresh install apps with a handul of updates take less than 1 minute to push code, database and files back up to Pantheon.
* If you are going to be pulling a larger website on Pantheon and want to get working right away - choose NOT to download database and files when using the GUI or

<pre><code class="language-bash">
// If using Kalabox CLI
kbox create pantheon -- -v --site=big-brand-here --env=dev --nodb --nofiles --name=big-brand-here --dir=/Users/yournamehere/.kalabox/apps

// Or to place the App in your Mac OS Sierra 'Documents' Cloud Storage
kbox create pantheon -- -v --site=big-brand-here --env=dev --nodb --nofiles --name=big-brand-here --dir=/Users/yournamehere/Documents/Sites
</pre></code>


* Instead you should take advantage of Pantheon's built in Backup system and download your Database and Files as individual downloads and them place them in your app manually

<pre><code class="language-bash">
// By default here
/Users/yournamehere/.kalabox/apps/files/...
</pre></code>

* After you download your large database from Pantheon, you will need to manually upload into your Kalabox virtual database
* You can easily get all your Kalabox database connection information from the Kalabox GUI by clicking 'connection info' or use the Kalabox CLI

<pre><code class="language-bash">
// Change directory into your app
$ cd /Users/yournamehere/.kalabox/apps/big-brand-here/

// Get a list of services and connection information for your app
$ kbox services

// ex:
{
	"name": "db",
	"project": "big-brand-here",
	"external_connection_info": {
	  "database": "pantheon",
	  "user": "pantheon",
	  "password": "pantheon",
	  "host": "big-brand-here.kbox",
	  **"port": "32810"**
	}
},

</pre></code>

* Pay close attention to the database port number as this changes everytime you start your app
* You can now use this information in a thrid party Database Client like [Sequal Pro](https://www.sequelpro.com/) -> Import DB 

## Reality Check: Too many files for our virtual machine to keep track of

The Drupal community has contributed so many awesome modules to enhanace our websites, but like Uncle Ben said 

> "with great power comes great responsibility." 

By default, Kalabox will synchronize all code files from your virtual machine to your local shared files directory (one splendid file at a time). Let me repeat that... by default, each file in your virtual machine will be replicated into your local shared files directory.

[add picture of retro hypnosis art here]

Every time a change is made to 1 of those files, Unison, Virtual Box and Kalabox play fun little game called "WTF just happned" and then begins to scan each file in our repo to account for all possible changes. For anyone else using Drupal Commerce that can mean over 15 modules alone with a vanilla install, not to mention the other 20 contributed modules and the handful of custom modules you created. You also have all of Drupal Core, Librararies, etc. This can lead to hundreds if not thousands of files for our app to keep track of. At one point in time, I made a change to code on my local machine and waited over 3 minutes for the change to appear in my local Kalabox app web browser (this included multiple refreshes and cach clearing from GUI and Drush). Turns out I was not alone and Kalabox team has taken careful consideration to eleviate these pain points that will come from any virtualized development enviroment.  

### Pro Tip

* Fortunately we can tune Kalabox to not only look for changes in certain file paths, but also exclude certain files such as those used by front end development tools such as /node_modules/ in our theme directory
* Simply edit your app's 'kalabox.yml' - look for the 'sharing' section and edit these lines

<pre><code class="language-bash">
sharing:
    share: 'data:/code'
    ignore:
      - Name sites/default/files
      - Name *node_modules*
      - Name *bower_components*
      - Name *vendor*
      - Name *build*
    paths:
      - sites/all/modules/custom
      - sites/all/themes/big-brand-theme
</pre></code>

* If you really want to speed up your app creation process - stop your newly created Kalabox app as soon as it is created by pressing the stop button on the GUI or

<pre><code class="language-bash">
// From the Kalabox CLI
$ kbox stop
</pre></code>

* This will in effect stop Kalabox from trying to sync all your files from virtual machine to your local shared files directory
* Make sure you tune your app's 'kalabox.yml' as described above
* Turn your Kalabox app back on using the power button on the GUI or

<pre><code class="language-bash">
// From the Kalabox CLI
$ kbox start
</pre></code>

* You will now notice your apps file structure just got a lot smaller, by only synchronizing your allowed paths from the 'kalabox.yml'
* This keeps your code base lean and your Dev Team can focus on their given feature or theme development

## Reality Check: What About The Files That Are NOT Synchrozed?

There is a bit of gingerly dance at play here. We are tuning our 'kalabox.yml' so that we are developing, making code changes, and seeing the results of those changes in our virtual machine in near real time, but often times we discover we need to add another contributed module or library that is outsode of our designated 'kalabox.yml' paths. Trust me - this happens all too often. 

Kalabox has some awesome built-in Dev tools that work directly on the virtual machine such as: git, bower, gulp and drush ([full list of Pantheon Dev tools here](http://pantheon.kalabox.io/en/stable/users/tooling/)). Lets say you wanted to use drush to download and install the 'admin_menu' module:

<pre><code class="language-bash">
// From the Kalabox CLI
$ kbox drush en -y admin_menu
</pre></code>

At this point your kalabox app will have downloaded and installed the 'admin_module' directly to your /sites/all/modules/contrib/ folder on your virtual machine. The best part is we don't need to wait to have those files to be scynchronized to our local shared files directory before they will work in our app because we explicitly told kalabox ONLY to synch files as described in our 'kalabox.yml' file. Drush is amazingly fast, so just wait till it's done and refresh your app int he browser. BoOm! It just works.

### Pro Tip

* If you do in fact need to patch that contrib module, you have a few more options:

* Update your 'kalabox.yml' to include the exact path to your module -> then restart your app

<pre><code class="language-bash">
// From the Kalabox CLI
$ kbox restart
</pre></code>

* You can also choose to use Pantheon's built in SFTP connection and upload files like settings files, contrib modules and libraries directly to the server then do a quick pull of those changes back into your local kalabox app

<pre><code class="language-bash">
// From the Kalabox CLI
$ kbox git pull
</pre></code>

* Most of the time we don't ever change the code of these type of files so we found that it was easier to by-pass file synchronization and just let the virtual machine handle those files


## Reality Check: Pantheon MultiDev and Git Branches

Pantheon's MultiDev environments are awesome for isolating development features, testing out global site changes and working with a team of developers. In reality they are isolated site environments for git branches. If you wanted the true Pantheon MultiDev experience you would create a new Kalabox app for each Pantheon MultiDev. We personally think this is overkill for our agency and team work flow. If we have a new team member added to the project, we recommend they clone their app from a MultiDev that we have set up for them. This keeps their work isolated and can push upstream only with proper credenctials. Most of the time we just create the app from a clone of DEV enviroment and use git to switch to MultiDev branches. Most of time we are mainly working on code changes so database and files rarely need to be the most current for us to be able to develop with confidence.

### Pro Tip

* If you are mainly working with code changes - keep it simple and just create 1 single app to rule them all
* Use 'kbox git checkout' to swicth between branches

## Reality Check: Front End Web Development with Kalabox

As mentioned before, Kalabox has some great front end dev tools built into the app so that we can take advantage of things like Gulp Sass to be applied directly on the virtual machine. What we came to discover is that there are many factors that will determine the overall performance of your development. Computer age, speed, RAM, RAM Cache, web browsers, gulp procecedures, gulp commands and syncronized 'kalabox.yml' file paths will all greatly effect the performance of your development.

### Pro Tip

* Keep the Gulp procedures to a minimum - if you don't need Babel or Uglify on this project - don't use it
* Gulp 'watch' is FASTER in the long run than single gulp commands such as 'kbox gulp sass'
* The first time you run 'kbox gulp watch' -> it will take a while (close to 30 seconds depending on your gulp procedures)
* After the first Gulp has completed they will dramatically reduce in latency
* We found it was best to onboard new Devs to Kalabox by having them download the app, install it, open up the GUI for the first time (this helps them associate our project to Kalabox from a visual queue) -> create new app from Pantheon MultiDev without downloading files and database -> once it is done -> turn off the app -> tune the 'kalabox.yml' -> continue app management using the CLI using the manual import of Database and files as described above.

## Reality Check: Onboarding New Devs to Your Project and Kalabox

This post originally came about as a form of onboarding, to help reduce the time it took to get new team developers up to speed on what Kalabox was and how to best confure it so we can set up quickly and expect consistent results. Here are a few takeaways to help your team get up to speed quickly. 

### Pro Tip

* Have new Devs download Kalabox before they come in
* Setup their Pantheon acccount before the sprint and add them to the project with appropriate organizational role
* Have your team turn off their computers before they walk into the sprint
* This eleviates all the extra background processes that might be lurking in the background wasting ram (we like to call them gremlins)
* Chrome tabs are a RAM killer, have your team be aware of their RAM usage and availability
* We highly recommend ['Memory Clean'](https://itunes.apple.com/us/app/memory-clean-monitor-free/id451444120?mt=12) for Mac - it's free and amazing
* Tune your 'kalabox.yml' so that only specific folders are being watched
* If they are a themer - expose the theme path, if they are custom coding a feature or extending a module, expose the /custom/ module path only

## Live Long and Kalabox

We are super excited for the latest realease of Kalabox. If you are new to Kalabox - go download it now! Trust me. If you ever tried Kalabox 1 or Kalabox 2 while in Beta - go dowload the latest version now! The bugs are gone and it's blazing fast! You're welcome.

- Love Gonz.