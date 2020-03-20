## Confusing Terms in the Git Terminology

Git and GitHub are at the core of open source in today's scenario. However, there are a lot of confusing terms that often seem similar yet can have conflicting meanings and uses. Let's eradicate these confusing terms by decoding their underlying meanings and sense.

- ### Origin and Upstream

From Git Documentation:
> When a repo is cloned, it has a default remote called origin that points to your fork on GitHub, not the original repo it was forked from.

>To keep track of the original repo, you need to add another remote named upstream

This confusion arises when you are working on the clone of a forked repo. **Upstream** is what you would use to **fetch from the original repo** in order to keep your local copy in sync with the project you wanted to contributed to. Meanwhile, **Origin** is what you would use to **pull and push code to your own fork** and thereafter you can contribute back to the upstream repo by making a pull request.

![Upstream and origin](https://i2.wp.com/i.stack.imgur.com/L5wRU.png)
source: [https://stackoverflow.com](https://stackoverflow.com)

**Remember**: Remotes are simply an alias that store the URL of repositories.

- ### Fetch and Pull

From Git Documentation:
> git fetch can fetch from either a single named repository or URL, or from several repositories at once.

>git pull incorporates changes from a remote repository into the current branch.

**git fetch** is the command that tells your local git to retrieve the latest meta-data info from the original yet doesn’t do any file transferring. It’s more like just checking to see if there are any changes available. **git pull** on the other hand does that AND copies those changes from the remote repository.

![fetch vs pull](https://i.stack.imgur.com/nWYnQ.png)
source: [https://stackoverflow.com](https://stackoverflow.com)

**Remember**:  `git pull` is shorthand for `git fetch` followed by `git merge FETCH_HEAD`

Putting it rather simply, **git fetch** can be used to know the changes done in the remote repo/branch since your last pull. This is useful to allow for checking before doing a **git pull**, which could change files in your current branch and working copy and potentially lose your changes, etc.

- ### Switch and Checkout

From Git Documentation:
>git switch switches to a specified branch. The working tree and the index are updated to match the branch.

>git checkout updates files in the working tree to match the version in the index or the specified tree

`git switch` is not a new feature but an additional command to switch/change branch feature which is already available in the overloaded `git checkout` command. Hence, to separate out the functionalities, the **Git 2.23** introduced the new git switch branch command which is an attempt to start to scale back to the responsibilities without breaking backward compatibility.

![switch vs checkout](https://bluecast.tech/wp-content/uploads/2019/09/git_switch_branch_vs_git_Checkout_branch-1024x521.png)
source: [https://bluecast.tech](https://bluecast.tech)

- ### HEAD~ and HEAD^

The **~(tilde)** and **^(caret)** symbols are used to point to a position relative to a specific commit. The symbols are used together with a commit reference, typically **HEAD**(represents the current snapshot of a branch) or a commit hash.

![HEAD^ vs HEAD~](https://backlog.com/app/themes/backlog-child/assets/img/guides/git/collaboration/switch_branches_001.png)
source: [https://backlog.com](https://backlog.com)

`~n` refers to the nth grandparent. `HEAD~1` refers to the commit's first parent. `HEAD~2` refers to the first parent of the commit's first parent.

`^n` refers to the the nth parent. `HEAD^1` refers to the commit's first parent. `HEAD^2` refers to the commit's second parent. A commit can have two parents in a merge commit.

That's all for this article. I hope that it would have helped to demystify some of the confusing terminologies related to git and GitHub. Please comment your valuable suggestions and feedback.

In case you want to connect with me, follow the links below:


[LinkedIn](https://www.linkedin.com/in/pragati-verma-b22a1b17b/) | [GitHub](https://github.com/PragatiVerma18) | [Twitter](https://twitter.com/Pragati56242726) | [Instagram](https://www.instagram.com/pragativerma18/) | [Medium](https://medium.com/@itispragativerma)

