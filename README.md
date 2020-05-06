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
 
 2. go to jenkins create 4 job 
    job1 for deploy code on webserver_testing environment 
    job2 for deploy code on weserver production environment
    job3 for depends on job1 as soon as job1 code deploy docker production system run
    job4 for depends on job2 as soon as testing team confirm testing then testing environment system run
    ### when testing job running great then one more job trigger to git and merge both master barcnh and dev1 branch 
    
    
3.  use the above 3 git command ,when you think dev and master work is ok merge them ,and send it to production environment (master->github->wehook->jenkins->production server by docker).
