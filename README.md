Git-Mrt-Map
===========

Git for MRT map

1) In the beginning, I let <other branch> to go to the transit point first by "commit"
   Then, use the <main branch> to merge it as following:

   (Tamsui) touch Zhongshan
            git add Zhongshan
            git commit -am "Zhongshan"
            git checkout master
   # master branch stays at Beimen --> Songshan
   (master) git merge Zhongshan --no-ff
            
   However, this approach will create two "Songshan" nodes, one is from Tamsui branch
   The other one is from the merge of master and Tamsui branches

OR

   We do not need to move <Tamsui> branch to the transit station
   What we have to do is to merge directly with --no-ff

   # Tamsui stays at Taipei Main Station --> Tamsui
   (Tamsui) git log     # checkout your current station
            git checkout master

   # master stays at Beimen --> Songshan
   # I want to use <master> branch to merge(fast forward) to other branch
   (master) git merge Tamsui --no-ff
            # Add "Zhongshan" to the merge comment
   # Then, you will see one Zhongshan node only!!!

   PS. You can use either master branch or Tamsui branch to merge for the transit station

   This way you will leave the <Tamsui> branch points to its previous node but
   <master> branch moves forward to the new merge point (Zhongshan: Tamsui and master)

   So, you can create a new branch from that merge point to continue the task

   (master) git branch branchname <sha1-of-commit>

2) 
   2a. If you want to move backward

       (master) git reset --hard <commit hex value>

       Note: <commit hex value>: you can know this value from git log

   2b. Git rename branch
       $ git branch -m <oldname> <newname>
       
       If you want to rename the current branch, you can simply do:
       $ git branch -m <newname>


3) It takes some time to finish it
   However, you can write a script to type the command for you

4) I'll paste the history file for reference2) It takes some time to finish it
   However, you can write a script to type the command for you

3) I'll paste the history file for reference

