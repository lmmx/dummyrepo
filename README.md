# dummyrepo
dummyrepo to test checkout hook compatibility with gitpython

```sh
git checkout master
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
