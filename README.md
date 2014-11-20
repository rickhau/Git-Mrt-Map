Git-Mrt-Map
===========

Git for MRT map

1) Deal with Merge points(Transit Station)

- Create two nodes for transit station:

  Move `<other branch>` to go to the transit point first by "commit"

  Then, checkout to the `<main branch>` to merge it as following:

```bash
   (Tamsui) touch Zhongshan
            git add Zhongshan
            git commit -am "Zhongshan"
            git checkout master
   # master branch stays at Beimen --> Songshan
   (master) git merge Zhongshan --no-ff
```
            
   However, this approach will create two **Songshan** nodes,

   One is from Tamsui branch, and the other one is from

   the merge of master and Tamsui branches which stays at master branch

Figure:
   
```
   -----<Tamsui>--------Zongshan
                             \
   ---<master>----------------Zongshan--------->                      
```
OR

- Stop your `<other branch>` to the merge point and create a new one from master

   We do not need to move `<Tamsui>` branch to the transit station.

   What we have to do is to merge directly with `--no-ff`

```bash

   # Tamsui stays at Taipei Main Station --> Tamsui
   (Tamsui) git log     # checkout your current station
            git checkout master

   # master stays at Beimen --> Songshan
   # I want to use <master> branch to merge(fast forward) to other branch
   (master) git merge Tamsui --no-ff
            # Add "Zhongshan" to the merge comment
   # Then, you will see one Zhongshan node only!!!
```

Figure:                                               
                                                                   
```
					(master)$ git checkout -b NewTamsui
									(Create new branch)     
 --<Tamsui>---TPE Station-     --<New Tamsui branch>-->
                          \   /
 --<master>----BeiMen-----Zongshan--------------> master
```

   PS. You can use either master or Tamsui branch to merge for the transit station

   This way you will leave the `<Tamsui>` branch points to its previous node(TPE Main Station) but  `<master>` branch moves forward to the new merge point (Zhongshan: Tamsui and master)

   So, you have to create a new branch from that merge point to continue the task
   
```bash
   (master) git checkout -b NewTamsui

if master HEAD has moved to new commit, you can use git log to query the SHA1 commit of Zongshan, then use the following command to create the new branch from there.

   (master) git branch branchname <sha1-of-commit>

   Ex:
   (master) git branch NewTamsui 8608c5c   
```

2) Git commands Review

   a. If you want to move backward

```bash

      (master) git reset --hard <commit hex value>

       Note: <commit hex value>: you can know this value from git log
```

   b. Git rename branch
```bash
      $ git branch -m <oldname> <newname>
       
      If you want to rename the current branch, you can simply do:
      $ git branch -m <newname>
```
   c. Push all branches and tags
```bash
      $ git push --all origin
```
   d. If your local repository is older than remote, please do take this very carefully
      to force the remote push with **-f** option

```bash
      $ git push -f origin master
    OR
      push multiple branches
      $ git push --all -f origin
```
- Screenshot of GitX

  ![Gitx picture](/gitx.png)
     

-  It takes some time to finish it but this is a good topic to practice `Git` commands!!

   However, you can write a script to type the command for you

-  I do not use the consistent method to deal with merge points(transit stations)
   Meaning, the git map is mixed with two ways.


