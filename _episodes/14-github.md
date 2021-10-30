---
title: Hosting on GitHub
teaching: 45
exercises: 0
questions:
- "How do I share my changes with others on the web?"
objectives:
- "Explain what remote repositories are and why they are useful."
- "Push to or pull from a remote repository."
keypoints:
- "A local Git repository can be connected to one or more remote repositories."
- "Use the SSH protocol to connect to remote repositories."
- "`git push` copies changes from a local repository to a remote repository."
- "`git pull` copies changes from a remote repository to a local repository."
---

Version control really comes into its own when we begin to collaborate with
other people.  We already have most of the machinery we need to do this; the
only thing missing is to copy changes from one repository to another.

Systems like Git allow us to move work between any two repositories.  In
practice, though, it's easiest to use one copy as a central hub, and to keep it
on the web rather than on someone's laptop.  Most programmers use hosting
services like [GitHub](https://github.com), [Bitbucket](https://bitbucket.org) or
[GitLab](https://gitlab.com/) to hold those main copies; we'll explore the pros
and cons of this in a later episode.

Let's start by sharing the changes we've made to our current project with the
world.  Log in to GitHub, then click on the icon in the top right corner to
create a new repository called `planets`:

![Creating a Repository on GitHub (Step 1)](../fig/github-create-repo-01.png)

Name your repository "planets" and then click "Create Repository".

Note: Since this repository will be connected to a local repository, it needs to be empty. Leave 
"Initialize this repository with a README" unchecked, and keep "None" as options for both "Add 
.gitignore" and "Add a license." See the "GitHub License and README files" exercise below for a full 
explanation of why the repository needs to be empty.

![Creating a Repository on GitHub (Step 2)](../fig/github-create-repo-02.png)

As soon as the repository is created, GitHub displays a page with a URL and some
information on how to configure your local repository:

![Creating a Repository on GitHub (Step 3)](../fig/github-create-repo-03.png)

This effectively does the following on GitHub's servers:

~~~
$ mkdir ssb_test
$ cd ssb_test
$ git init
~~~
{: .language-bash}

Note that our local repository still contains our earlier work on `mars.txt`, but the
remote repository on GitHub appears empty as it doesn't contain any files yet.

The next step is to connect the two repositories.  We do this by making the
GitHub repository a [remote]({{ page.root}}{% link reference.md %}#remote) for the local repository.
The home page of the repository on GitHub includes the string we need to
identify it:

![Where to Find Repository URL on GitHub](../fig/github-find-repo-string.png)

Click on the 'SSH' link to change the [protocol]({{ page.root }}{% link reference.md %}#protocol) from HTTPS to SSH.

> ## Using SSH
>
> We use SSH here because, while it requires some additional configuration, it is a 
> security protocol widely used by many applications.  The steps below describe SSH at a 
> minimum level for GitHub. A supplemental episode to this lesson discusses advanced setup 
> and concepts of SSH and key pairs, and other material supplemental to git related SSH. 
{: .callout}

![Changing the Repository URL on GitHub](../fig/github-change-repo-string.png)

Copy that URL from the browser, go into the local `ssb_test` repository, and run
this command:

~~~
$ git remote add origin git@github.com:DeepsMoseli/ssb_test.git
~~~
{: .language-bash}

Make sure to use the URL for your repository rather than Vlad's: the only
difference should be your username instead of `vlad`.

`origin` is a local name used to refer to the remote repository. It could be called
anything, but `origin` is a convention that is often used by default in git
and GitHub, so it's helpful to stick with this unless there's a reason not to.

Using HTTPS

~~~
$ git clone https://github.com/DeepsMoseli/ssb_test.git
~~~
{: .language-bash}

~~~
Cloning into 'ssb_test'...                                                                                              remote: Enumerating objects: 6, done.                                                                                   remote: Counting objects: 100% (6/6), done.                                                                             remote: Compressing objects: 100% (3/3), done.                                                                          remote: Total 6 (delta 0), reused 0 (delta 0), pack-reused 0                                                            Unpacking objects: 100% (6/6), 1.23 KiB | 3.00 KiB/s, done.
~~~
{: .output}

We can check that the command has worked by running `git remote -v`:

~~~
$ git remote -v
~~~
{: .language-bash}

~~~
origin   git@github.com:DeepsMoseli/ssb_test.git (fetch)
origin   git@github.com:DeepsMoseli/ssb_test.git (push)
~~~
{: .output}

We'll discuss remotes in more detail in the next episode, while
talking about how they might be used for collaboration.

## Push local changes to a remote

We can now return to the remote.  This command will push the changes from
our local repository to the repository on GitHub:

~~~
$ git push origin main
~~~
{: .language-bash}

~~~
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (6/6), 1.45 KiB | 372.00 KiB/s, done.
Total 16 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), done.
To https://github.com/DeepsMoseli/ssb_test.git
 * [new branch]      main -> main
~~~
{: .output}

> ## Proxy
>
> If the network you are connected to uses a proxy, there is a chance that your
> last command failed with "Could not resolve hostname" as the error message. To
> solve this issue, you need to tell Git about the proxy:
>
> ~~~
> $ git config --global http.proxy http://user:password@proxy.url
> $ git config --global https.proxy https://user:password@proxy.url
> ~~~
> {: .language-bash}
>
> When you connect to another network that doesn't use a proxy, you will need to
> tell Git to disable the proxy using:
>
> ~~~
> $ git config --global --unset http.proxy
> $ git config --global --unset https.proxy
> ~~~
> {: .language-bash}
{: .callout}

> ## Password Managers
>
> If your operating system has a password manager configured, `git push` will
> try to use it when it needs your username and password.  For example, this
> is the default behavior for Git Bash on Windows. If you want to type your
> username and password at the terminal instead of using a password manager,
> type:
>
> ~~~
> $ unset SSH_ASKPASS
> ~~~
> {: .language-bash}
>
> in the terminal, before you run `git push`.  Despite the name, [Git uses
> `SSH_ASKPASS` for all credential
> entry](https://git-scm.com/docs/gitcredentials#_requesting_credentials), so
> you may want to unset `SSH_ASKPASS` whether you are using Git via SSH or
> https.
>
> You may also want to add `unset SSH_ASKPASS` at the end of your `~/.bashrc`
> to make Git default to using the terminal for usernames and passwords.
{: .callout}

Our local and remote repositories are now in this state:

![GitHub Repository After First Push](../fig/github-repo-after-first-push.svg)

> ## The '-u' Flag
>
> You may see a `-u` option used with `git push` in some documentation.  This
> option is synonymous with the `--set-upstream-to` option for the `git branch`
> command, and is used to associate the current branch with a remote branch so
> that the `git pull` command can be used without any arguments. To do this,
> simply use `git push -u origin main` once the remote has been set up.
{: .callout}

We can pull changes from the remote repository to the local one as well:

~~~
$ git pull origin main
~~~
{: .language-bash}

~~~
From https://github.com/vlad/planets
 * branch            main     -> FETCH_HEAD
Already up-to-date.
~~~
{: .output}

Pulling has no effect in this case because the two repositories are already
synchronized.  If someone else had pushed some changes to the repository on
GitHub, though, this command would download them to our local repository.

> ## GitHub GUI
>
> Browse to your `ssb_test.git` repository on GitHub.
> Under the Code tab, find and click on the text that says "XX commits" (where "XX" is some number).
> Hover over, and click on, the three buttons to the right of each commit.
> What information can you gather/explore from these buttons?
> How would you get that same information in the shell?
>
> > ## Solution
> > The left-most button (with the picture of a clipboard) copies the full identifier of the commit 
> > to the clipboard. In the shell, ```git log``` will show you the full commit identifier for each 
> > commit.
> >
> > When you click on the middle button, you'll see all of the changes that were made in that 
> > particular commit. Green shaded lines indicate additions and red ones removals. In the shell we 
> > can do the same thing with ```git diff```. In particular, ```git diff ID1..ID2``` where ID1 and 
> > ID2 are commit identifiers (e.g. ```git diff a3bf1e5..041e637```) will show the differences 
> > between those two commits.
> >
> > The right-most button lets you view all of the files in the repository at the time of that 
> > commit. To do this in the shell, we'd need to checkout the repository at that particular time. 
> > We can do this with ```git checkout ID``` where ID is the identifier of the commit we want to 
> > look at. If we do this, we need to remember to put the repository back to the right state 
> > afterwards!
> {: .solution}
{: .challenge}

> ## Uploading files directly in GitHub browser
>
> Github also allows you to skip the command line and upload files directly to 
> your repository without having to leave the browser. There are two options. 
> First you can click the "Upload files" button in the toolbar at the top of the
> file tree. Or, you can drag and drop files from your desktop onto the file 
> tree. You can read more about this [on this GitHub page](https://help.github.com/articles/adding-a-file-to-a-repository/)
{: .callout}

> ## GitHub Timestamp
>
> Create a remote repository on GitHub. Push the contents of your local
> repository to the remote. Make changes to your local repository and push these
> changes. Go to the repo you just created on GitHub and check the
> [timestamps]({{ page.root }}{% link reference.md %}#timestamp) of the files. How does GitHub
> record times, and why?
>
> > ## Solution
> > GitHub displays timestamps in a human readable relative format (i.e. "22 hours ago" or "three 
> > weeks ago"). However, if you hover over the timestamp, you can see the exact time at which the 
> > last change to the file occurred.
> {: .solution}
{: .challenge}

> ## Push vs. Commit
>
> In this episode, we introduced the "git push" command.
> How is "git push" different from "git commit"?
>
> > ## Solution
> > When we push changes, we're interacting with a remote repository to update it with the changes 
> > we've made locally (often this corresponds to sharing the changes we've made with others). 
> > Commit only updates your local repository.
> {: .solution}
{: .challenge}

> ## GitHub License and README files
>
> In this episode we learned about creating a remote repository on GitHub, but when you initialized 
> your GitHub repo, you didn't add a README.md or a license file. If you had, what do you think 
> would have happened when you tried to link your local and remote repositories?
>
> > ## Solution
> > In this case, we'd see a merge conflict due to unrelated histories. When GitHub creates a 
> > README.md file, it performs a commit in the remote repository. When you try to pull the remote 
> > repository to your local repository, Git detects that they have histories that do not share a 
> > common origin and refuses to merge.
> > ~~~
> > $ git pull origin main
> > ~~~
> > {: .language-bash}
> >
> > ~~~
> > warning: no common commits
> > remote: Enumerating objects: 3, done.
> > remote: Counting objects: 100% (3/3), done.
> > remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
> > Unpacking objects: 100% (3/3), done.
> > From https://github.com/vlad/planets
> >  * branch            main     -> FETCH_HEAD
> >  * [new branch]      main     -> origin/main
> > fatal: refusing to merge unrelated histories
> > ~~~
> > {: .output}
> >
> > You can force git to merge the two repositories with the option `--allow-unrelated-histories`. 
> > Be careful when you use this option and carefully examine the contents of local and remote 
> > repositories before merging.
> > ~~~
> > $ git pull --allow-unrelated-histories origin main
> > ~~~
> > {: .language-bash}
> >
> > ~~~
> > From https://github.com/vlad/planets
> >  * branch            main     -> FETCH_HEAD
> > Merge made by the 'recursive' strategy.
> > README.md | 1 +
> > 1 file changed, 1 insertion(+)
> > create mode 100644 README.md
> > ~~~
> > {: .output}
> >
> {: .solution}
{: .challenge}
