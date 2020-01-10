---
title: Git
weight: 5
chapter: true
---

## Tips
* To combine git add, commit and push in one command, per[git add, commit and push](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one)

    ```
    git config --global alias.cmp '!f() { git add -A && git commit -m "$@" && git push origin master; }; f'
    ```



