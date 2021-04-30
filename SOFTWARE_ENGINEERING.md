# Guide to software engineering in the Lowe lab

:construction: Work in Progress :construction:

Sections
* [Python](#python)
* [Documentation](#documentation)
* [Tests](#tests)
* [Using github](#using-github)


"The Turing Way" is an amazing open-source guide to software development and data science. I recommend that you take a look:
https://the-turing-way.netlify.app/welcome

---

# Python

---

# Documentation

We are following the `numpy` style guidelines:  
https://numpydoc.readthedocs.io/en/latest/format.html#overview

---

# Tests

---

# Using github

## Setting up your fork of an existing project

First fork the repo on github.  When you have created your fork, clone it so that you have a local copy:

```sh
git clone https://github.com/your-github-username/<repo name>.git
cd <repo name>
```

Next, you need to link it to the main repo:
```sh
git remote add upstream https://github.com/quantumjot/<repo name>.git
```
**This is important**, because it enables you to keep your fork up-to-date with everyone's changes.

Finally, all the code needs to be free from errors and in the same style. This is achieved by setting  up the `pre-commit` hooks:
```sh
pre-commit install
```
Now, when you commit changes to your branch, they will automatically be checked for style and errors. You may need to install `pre-commit`:

```sh
pip install pre-commit
```

## Making a new branch

If your want to contribute your new feature, make sure to make a new branch:
```sh
git checkout master -b your-branch-name
```

Use the following to determine which branch you're on:
```sh
git status
```

## Keeping your fork up to date
The following commands will update the main branch of your fork:
```sh
git checkout master
git pull upstream master
```

You can then update any branches by:
```sh
git checkout your-branch-name
git merge master
```
