# dummyrepo

dummyrepo to test checkout hook compatibility with gitpython

- copy the script [here](https://gist.github.com/wizioo/c89847c7894ede628071)
  to `.git/hooks/post-checkout`
- `chmod 755 .git/hooks/post-checkout`
- `cp .gitignore.master .git/info/exclude` (or `git checkout www; git checkout master`)

The following routine will stash (push) some files created in the `master` branch
then pop them after checking out the `www` branch. Only one directory is stashed
(its "pathspec" identifies it in the master branch, before the checkout).

This directory is deliberately placed in a branch-specific `.gitignore`,
so there is no risk of it accidentally being pushed to the wrong branch.

The stash includes ignored files (`--all`), allowing the directory to be moved in this way.

```sh
# git checkout master
mkdir webfiles
echo 1 > webfiles/a.txt 
echo 2 > webfiles/b.txt 
echo 3 > webfiles/c.txt 
git stash push --all -- webfiles/
git checkout www
ls webfiles/
rm -rf webfiles/
git stash pop
ls webfiles/
```

A file that has been committed and pushed to the `master` branch can be copied over
to the `www` branch by the following routine (using the example of this README):

```sh
git checkout www
rm README.md 
git checkout --theirs master README.md
gadd
git commit -m "Update README; add stashed/popped files"
git push origin www
```
