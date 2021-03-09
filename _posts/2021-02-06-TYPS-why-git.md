---
published: false
---

# **TYPS** - Why git

![git](https://git-scm.com/images/logos/1color-orange-lightbg@2x.png)

More and more university courses in economics have started teaching students how to use git, and why using it is extremely valuable. My coauthor [Jeppe Druedahl](https://sites.google.com/view/jeppe-druedahl/home), for example, shares material of his advanced classes via GitHub, and encourages students to create a well-structured repository for their assigments and course projects.

I was not so lucky. Most of my former colleagues at economics department do not use git, nor they know why they would use it.

## Starting from zero

The goal of this post is to show how we use it in our team, and why it is useful to us. [Ahdering to my own guidelines for **TYPS**](http://alemartinello.com/2021/02/17/TYPS-what/), I will not explain how git works or how a software developer uses it. There's plenty of good guides for that, first and foremost [Git's own documentation](https://git-scm.com/doc).

My goal will be instead to show why even the most basic usage of git can be extremely useful for researchers and data analysis, giving a few practical examples.

## Why version control?

Git is a version control software, which might beg the question of what is version control at all. Version control is the practice of simply keeping track of changes in your code.

Simply having a folder where you keep old versions of files is techincally a form of version control. Most people do it all the times for word and powerpoint documents. I used to back-up my do-files every once in a while.

    root/
    ├── my_script.do
    ├── backup/
    │   ├── my_script_20200601.do
    │   ├── my_script_20200913.do
    │   ├── my_script_20201129.do
    │   ├── my_script_20210120.do

This system is however a pretty bad version of version control. You can hardly keep track of what exactly changed across versions, and the "*every once in a while*" is rather dangerous. Way too often I saved backups of files where multiple things changed at once, and tracing back why my results suddently changed was a mess.

Git induces you to be much more systematic in your versioning, and allows to trace back specific changes in your code. While it really shines when collaborating wth other people, it can greatly help you even on a solitary project.

## Using git on a project where you are the only developer

I like to imagine git as a system of checkpoints in a videogame. Every time you reach a milestone, you write a specific function, or you construct a class, you get the chance of saving a checkpoint of your work. That's amazingly useful even if you work alone.

First, you never have to worry
