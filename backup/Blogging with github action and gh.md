# How to post with gh

> Purpose
> Record the post method

## List post

```sh
gh issue list
```

## New post

```sh
# This backup file is created by github actions, there I just use the file for edit.
# -t title, -l label, -F File
gh issue create -t test -l autoscript -F .\backup\draft.md
# -b body
gh issue create -t test -l autoscript -b 'This is the body'
```

## View post

```sh
gh issue view 3
gh issue view 3 --web
```

## Edit post

```sh
# modify the title and body of the number 5 issue.
gh issue edit 5 -t autoscript -b 'short body'
```

## Delete post

```sh
gh issue delete 5
```

## New label

```sh
gh label create name
```

