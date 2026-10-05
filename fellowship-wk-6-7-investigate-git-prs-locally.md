# Git Command to Investigate Open-Source Pull Requests

When getting into open-source development, the usual recommendation is to look for issues tagged as "good first issue."
However, in some projects (such as Bitcoin Core), issues aren't necessarily labeled in that way.

Another good starting point then is to review pull requests (PRs). As a reviewer, you want to look into the proposed code change and ask yourself and the author some critical questions to help maintainers decide which PRs are ready to be merged, and which maybe need more work.

In this article I am focusing on how I prefer to check out pull requests to run the code and test them locally. But there is of course more to say about the review process. I will provide links for further reading by bitcoin-core contributors further below. If you're not into bitcoin-core, their insight is still valuable as it is one of the most decentralized open-source codebases out there. They are living it and are seeing what works and what does not.

## What is the Goal?
To know where I'm going here, let's take a look at the end. The goal is to run local inspection commands like these:

```bash
git fetch upstream pull/<PR_ID>/head:<BRANCH_NAME>
git switch <BRANCH_NAME>
```

The first command fetches the remote PR data, and the second switches your local copy to it. Let's break down how this works under the hood and look at an optimized shortcut to speed up your daily engineering loop.  
... and as bonus to then improve on those commands to make it shorter.

## Git Fetch Command

Before going further, let's focus on the three parts: `<PR_ID>`, `<BRANCH_NAME>`, and `upstream`.

### PR ID & Branch Name
* `<PR_ID>` is the pull request ID.
  On GitHub, it is the number shown after the `#` symbol, displayed after the title.
* `<BRANCH_NAME>` is your local branch name and can be anything you want.
  The sensible choice is to give it a name you'd recognize, such as `pr_1234`. But you can call it `strawberries_yum` instead if you really, really like them.

GitHub has their own excellent docs describing how to [check out PRs locally](https://docs.github.com/en/pull-requests/how-tos/review-pull-requests/checking-out-pull-requests-locally). You will notice, though, that they refer to `origin` instead of `upstream`. So let's look into that.

### Origin vs. Upstream
GitHub shows `origin` in their documentation because typically we would be working inside the same repository that we originally cloned. When running `git clone ...`, Git automatically maps that source repository as our default remote location, naming it `origin`.

However, when working as an open-source contributor on a large project (such as bibtcoin-core), the contributor workflow more often than not require us to fork the project in our own GitHub space. And we then push code changes as raised pull requests from this fork. For such a setup we would want to have multiple Git remotes set up:
* `origin` is then our fork from which we cloned to our local machine, and
* `upstream` points to the repository located "upstream" from your fork that we want to contribute to.

## Configuring an Upstream Remote

To pull code changes and pull requests from the main repository, we link it locally as another remote. By convention, we call it `upstream`.

We can add upstream with Git like this:
```bash
git remote add upstream <repository_URL>
```

Depending on our GitHub auth preference, we replace `<repository_URL>` with either the SSH or HTTPS path (sticking with bitcoin as example):

* SSH Path: `git@github.com:bitcoin/bitcoin.git`
* HTTPS Path: `https://github.com`

Again, GitHub have their own docs with more information on [working with remotes](https://docs.github.com/en/get-started/git-basics/managing-remote-repositories).

And now we have arrived at our goal!  
We can fetch PRs by their number:
```bash
git fetch upstream pull/1234/head:pr/1234
git switch pr/1234
```
... and we're ready to build the code, run tests, etc.

### Objection! `gh` Can Do That

When discussing the above approach with my cohort of [Btrust fellows](https://blog.btrust.tech/introducing-the-2026-open-source-fellowship/), someone (shout out to you-know-who-you-are for that!) rightfully pointed out that GitHub's own CLI tool can do that right out of the box with:
```bash
gh pr co 1234
```
which even switches to the branch in one command. Neat!  
(I later figured out we'd also need to point to the different remote, but that's not relevant here.)

## Git Alias to the Rescue

I didn't use `gh` and hadn't planned on installing it just to check out PRs. But the point stood that it requires one command that does a lot of the lifting.  
As a result, I started putting together a `git alias` for that.

Adding the alias is then done like with this command:
```bash
git config --global alias.prco '!f() { git fetch ${2:-origin} pull/$1/head:pr/$1 && git switch pr/$1; }; f'
```

### Syntax and Usage
The alias take one mandatory `PR_ID` parameter and an optional `remote` parameter:

```bash
git prco <pr_ID> [<remote>]
```
Where `<remote>` defaults to `origin`.

In our context, checking out pull request `#1234` becomes this:

```bash
git prco 1234 upstream
```

## Native Alias vs. GitHub CLI (`gh`)

Using custom Git alias versus installing the official GitHub CLI tool comes with distinct trade offs. 

### Disadvantages of the Custom Alias
* Without `gh` installed, we don't get all the other goodies their wrapper provides.
* Using `gh`, we don't need to define `upstream` to do the same.
  (Instead, we add the `-R` flag.)

### Advantages of the Custom Alias
* We don't need to install gh (okay okay, that is a teeny tiny advantage only.)
* Checking out from a remote other than origin, it is actually shorter:
  * Custom Alias: `git prco 1234 upstream`
  * GitHub CLI: `gh pr co 1234 -R bitcoin/bitcoin`
* It should also work on Gitea, Forgejo and Codeberg. Not on GitHub exclusively.
* The remote parameter accepts standard aliases (`upstream`), direct HTTPS URLs (`https://github.com...`), or SSH paths (`git@github.com:...`), too.
  But those are clearly more cumbersome to type out than GitHub CLI's `-R <owner>/<repo>` option.

## Bonus Tip: One Alias to Rule Them All
As final touch, for use with Git aliases in general, I have defined another alias:

```ssh
git config --global alias.aliases config --get-regexp '^alias\.'
```

Calling `git aliases` then shows a list of all defined aliases. Not necessary, but useful as reminder if you start adding more aliases to your personal workflow.

## More Reading: Reviewing PRs

Now that we've made it easy to fetch and switch to pull requests' branches, we can benefit from insights on becoming a valued reviewer. What to look for, what to test, and how to communicate what we've found.

May the links below serve as starting point. And even if you're not interested in Bitcoin development yourself, the advice in the first two links will help any open-source project you want to support with your reviews:

- Jon Atack's [How to Review Pull Requests in Bitcoin Core](https://jonatack.github.io/articles/how-to-review-pull-requests-in-bitcoin-core)
- Gloria Zhao's [Review Checklist](https://github.com/glozow/bitcoin-notes/blob/master/review-checklist.md)
- Bitcoin Core PR Review Club's [README.md](https://github.com/Bitshala/BitcoinCore-PR-Review-Club)

So let's get out there and contribute.
