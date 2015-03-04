This project has two branches and one file.  The file is called file1.txt.  It contains three lines of text.

In the first commit the second line of text is:

```
I am going to change this line in two branches
```

In "master" I change the second line of text to:

```
I am going to BREAK this line in two branches
```

In "other" I change the second line of text to:

```
I am going to MODIFY this line in two branches
```

If I then do the following commands:

```
git checkout other
git checkout -b other-merge
git merge master
git checkout --theirs file1.txt
git commit -a -m "Where did the change from MODIFY to BREAK go?"
```

I can't see that my merge commit changed the word `MODIFY` to `BREAK`.  Normally I'd whip out the pickaxe and do this:

```
git log -S MODIFY
```

Or this:

```
git log -S BREAK
```

And I'd expect to see two changes.  One when it changed from `change` to `MODIFY` or `BREAK` and another when it changed from `MODIFY` back to `BREAK`.  However, I don't see that at all.  And if I do a `git show` on the merge commit I see nothing.  If I do a `git diff` on the two parent commits I do see the change though.

This makes it difficult to figure out when something changed because of a merge.  Instead of `git log -SMODIFY` I need to do this `git log -m -SMODIFY` and then it shows what I would expect.