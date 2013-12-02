---
author: admin
comments: true
date: 2012-04-04 21:25:16+00:00
layout: post
slug: hosting-your-own-git-repo-with-gitolite
title: Hosting your own git repo with Gitolite
wordpress_id: 290
categories:
- Git
- Gitolite
---

After using [CVS](http://en.wikipedia.org/wiki/Concurrent_Versions_System) (A.K.A. "Crappy Versions System") for way to long we decided to enter the twentieth century and move our code to [Git](http://git-scm.com/). We had used private Github repos for some smaller projects, but were reluctant to move the whole organizations code to Github, so we started to look for alternatives. We have a lot of consultants, partners and short term employees working with our code so we needed a good way of controlling access to the repos and preferrably without giving each of them a unix user on the server where the repo is hosted. And guess what, [Gitolite](http://sitaramc.github.com/gitolite/) gives us all that.


<!-- more -->


## What is Gitolite?




[Gitolite](http://sitaramc.github.com/gitolite/) is basically an access layer that sits on top of Git. Users are granted access to repos via a simple config file and you as an admin only needs the users public SSH key and a username from the user. Gitolite uses this to grant or deny access to your Git repositories. Gitolite is quite feature rich once you get to know it, but I will only cover the basic stuff here. The user guide is pretty good so make sure you check it out: [http://sitaramc.github.com/gitolite/](http://sitaramc.github.com/gitolite/).





## Installing Gitolite




First create a unix user called "git", then copy your SSH public key (from your workstation) to the server. Then, run these commands:




    
    <code class="language-bsh">git clone git://github.com/sitaramc/gitolite
    gitolite/src/gl-system-install
    gl-setup -q ~/YourName.pub
    </code>





Gitolite should now be installed on the server. I recommend setting up a separate domain name for the repo in case you want to move it later on, we chose "git.ourserver.com".





Now you need to clone Gitolite to your own workstation:




    
    <code class="language-bsh">git clone git@git.yourdomain.no:gitolite-admin.git
    </code>





The admin is very simple, there are basically two things you need to relate to: **keydir/** and **conf/gitolite.conf**




### Keydir




This is where Gitolite store all the users public keys. And as you can understand by now, most problems you are going to have with Gitolite is to get users to find/create and send you their SSH public key. Github currently has the best doc of [how to do this](http://help.github.com/mac-set-up-git/). The filename of the public key is going to be the username of the user so make sure you pick something that identifies the user in your organization. Here are some example users:




    
    <code class="language-bsh">/keydir/anders.pub
    /keydir/employee.pub
    /keydir/consultant.pub
    </code>





### The config




When you have the public key setup you need to create repos and give access to the users. The config file is located in **conf/gitolite.conf**. There are basically three concepts here, **groups**, **users** and **repos**. A group is prefixed with @ and a repo is prefixed with "repo ". Check out the following example config.




    
    <code class="language-bsh"># /conf/gitolite.conf
     
    @admin       =  anders
    @employees   = @admin employee1 employee2 employee3
    @consultants = @admin @employees consultant1 consultant2
     
    repo gitolite-admin
            RW+      =  @admin
    repo internal-project
            RW+      =  @employees
    repo comsultant-project
            RW+      =  @consultants
    
    </code>





In the config above, we have 3 groups: admin, employees and consultants. I chose to give access to groups instead of to individuals, but this simple file is actually quite powerful and gives you many ways of controlling access. It's also possible to only grant read access (**R**) and to not give users the possibility to rewind a branch (**RW**). **RW+** gives full access.





### Commit and push!




Next step is to commit and push the changes to the Gitolite admin. Gitolite will create the users and repos for you. 




    
    <code class="language-bsh">git add .
    git commit -m "Smart commit message goes here"
    git push
    </code>




If all goes well you should see a message from Gitolite that it has created the users and repos.




### Create a new repo 




So now you need to push your code to the new repo. If you do not already have a git repo locally that you want to upload, you need to create a new one:




    
    <code class="language-bsh">git init</code>





Then run **git status** to see the changes that are going to be commited. Make sure you have a sensible [.gitignore](http://help.github.com/ignore-files/) file set up to filter out IDE files, OS files and files from other versioning control systems. Then run **git add .** and **git commit -m "commit message"** to commit stuff to your local repo. But in order to commit to your Gitolite repo you need to first specify an origin:



    
    <code class="language-bsh">git remote add origin git@git.yourserver.com:projectname.git</code>





Makes sure the project name matches the name in **conf/gitolite.conf**. Then you need to commit to the new origin:



    
    <code class="language-bsh">git push origin master</code>





And that's it. The next (and maybe the hardest) step is to learn your users and employees how to send you their public key and to learn them Git... Good luck with that and happy coding!



