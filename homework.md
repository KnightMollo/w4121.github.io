---
layout: page
category : homework
---

## Getting Started with Git
If you are using git for the first time, you can use [Github's tutorial][2] to learn about Git. And for people want a bit more in-depth information, [Pro Git][1] is an excellent book which goes into details on using Git for daily code maintance, which you can [read online][1] for free.

**A fun fact** : Git is actually not that mysterious as many people might think, it's just a key value store (Dictionary, Hashmap) that does a bit smart calculation. Key is usually the SHA1 of your file, and value the content. Pro Git provides a chapter on demystifying Git.

## Git Repositories for Homework

You will use git a git server on dsvm01.cs.columbia.edu, both to clone the homeworks and to submit your work.
Here is what you have to do:

1. To get access to the homework, you need to email a plublic key (the .pub),
   named your-uni.pub, to the TA. To generate a public key if you don't have one, run `ssh-keygen -t rsa`. You don't have to put a password.
2. To access a specific homework, clone the repository, doing `git clone git@dsvm01.cs.columbia.edu:your-uni-hw-number`, for instance, my UNI is ml3302 so I would type `git clonegit@dsvm01.cs.columbia.edu:ml3302-hw2` for homework 2.
3. The assignment skeleton will be in the master branch.

<!--
## Homework Submission

1. To submit, just push your work to master. We will grade the most recent
   version in the master branch.
2. Submit your homework **before the deadline**. We will block commits after the
   precise deadline and you won't be able to submit anymore.

<a name="local"></a>

## How to test your code remotely
You need to ssh into the `clic-lab` cluster by using the following command:

~~~
ssh <uni>@clic-lab.cs.columbia.edu
~~~
The rest of the procedure is the same as if you were developing locally. Note that your home directory is NFS mounted. So it's the same everywhere no matter which machine in the cluster you have connected to.

## Attention
Make sure that you are working on the correct branch, so when we check the code out from your repository, it is contains the file that you have been working on.
-->


[1]: http://git-scm.com/book
[2]: http://try.github.io
[3]: http://ds-git.cs.columbia.edu
[4]: http://www.cs.columbia.edu/~crf/
[5]: https://www.virtualbox.org/wiki/Downloads
[6]: http://downloads.vagrantup.com/tags/v1.3.4
