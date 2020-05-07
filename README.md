# jenkinsintegration
jenkins integration with docker and web server

## 1. git branch :
``` git branch dev1  ------new dev1 branch craeted ```

how to create a branch ,and what is the need of it ,if we use    this then our critical environment (production are or client part) will give service without any break down.
## 2. git merge:
```git dev1 merge master ------branch merge to master branch ```
we know on a single project many people work so when we think that different developer done great ,we can merge ,it save our time in a project
## 3. git rebase:
``` git rebase master  -----update dev1 branch as like  master  ```
     when you check a specific developer work, if he is  back from master then go to  developer  branch and use
     git rebase master(main developer branch)
## 4 . git checkout:
``` git checkout dev1 ----switch to dev1 from master ```


# Integration 

 1. first go to git hub ,create a repository and webhook , webhook trigger when as soon as code commit 
 
 2. go to jenkins create testing_job
 ```for testing the web server ```
 
 3. then go to create one more job for QA-team-job
 ``` QA -team passing green single when testing is working good no error```
 
 4. then go to create one more job for Production-job
 ```after QA-team passing green single then Automatic trigger production job and deploy website for client```
  
 ## follow these steps:
job1 : For Testing Environment

SCM Git then enter the repo URL and branch dev1 
```Build Triggers - Poll SCM Build >Execute Shell > 
sudo cp -rvf * /lwweb 
if sudo docker ps | grep testing_webserver
then sudo docker rm -f testing_webserver
sudo docker run -dit -p 2021:80 -v /lwweb2:/usr/local/apache2/htdocs/ --name testing_webserver httpd
fi
``` 


job2 : For Production Environment

SCM Git then enter the repo URL and branch master 
```Build Triggers - Build after other projects are built > Projects to watch job3 Goto Build >Executive Shell > 
sudo cp -rvf * /lwweb 
if sudo docker ps | grep production_webserver 
then echo "Already Running" 
else sudo docker run -dit -p 2020:80 -v /lwweb:/usr/local/apache2/htdocs/ --name prodwebos httpd 
fi
``` 

job3 : For Quality Assuarance Team

SCM Git then enter the repo URL and branch dev1
```Additional Behaviours> Merge before build > Name of repository: origin Branch to merge to: master Merge Strategy: default Fast-forward mode: --ff Build Triggers - Trigger builds remotely (e.g., from scripts) Build >Execute Shell > 
#!/bin/bash 
echo "Build Sucessfull"
Post build Actions-
Check - Push only if build Succeeds Merge results
```
