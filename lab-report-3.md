---
layout: post
title: UNIX Commands
---

## Find
1. `find -cmin [time]`.
    
    This command shows all the files that have been changed in the specified amount of time, in minutes. This can be useful if you want to track your work and see everything you've changed in the last hour or so - especially useful if editing files that are not tracked by git!

    ![](images/lab-report-3/find1.png)

2. `find -size +[low] -size -[high]`

    This command shows all the files within a certain size range. This can be very helpful if you want to locate huge files that are clogging up your storage and delete them!

    ![](images/lab-report-3/find2.png)

3. `find -regex [pattern]`

    This command uses regex pattern matching to find files, which allows for a lot more options than simply expanding out stuff like "*.txt". For example, the example below shows all text files that start with a number and end with 17. Overall, regex allowes for much more customizable patterns.

    ![](images/lab-report-3/find3.png)

## Less
1. `less -N`

    This starts the less command but with each line being numbered. This is useful if you're editing a long file and you want to come back to a specific spot later. Instead of having to scroll through to find that spot, you can just remember the line number.

    ![](images/lab-report-3/less1.png)
    ![](images/lab-report-3/less2.png)

2. `less +[n] -j[N]`

    This command jumps to line `n` in the file positioned at the `Nth` line in the terminal. This is usefull because it can save some time scrolling if you already know where you want to go.

    ![](images/lab-report-3/less3.png)
    ![](images/lab-report-3/less4.png)

3. `less -p[pattern]`

    This command causes less to start at the first occurence of the patten. This is very useful if you are looking for a certain phrase in a file and you want to read the contents around that pattern; it saves some time from having to manually scroll through the file and look.

    ![](images/lab-report-3/less6.png)
    ![](images/lab-report-3/less5.png)