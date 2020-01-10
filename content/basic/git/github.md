+++
title = "Github"
weight = 10
+++

## Github setup
1. Signup account with Github and create a repo "tool", enable 2 step verification
1. Enable ssh connection to Github connect to Github through ssh [^1]

        # generate ssh keys
        cd ~/.ssh
        ssh-keygen -t rsa -C "wedgevine@outlook.com" -f "id_rsa_wedgevine"
1. [Adding a new SSH key to your GitHub account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)
1. Per [^1], create ~/.ssh/config file for each Github account
1. Setting the git remote Url for the local repositories

        cd local-repo
        git init
        git config user.name "wedgevine"
        git config user.email "wedgevine@outlook.com"
        git remote add origin git@wedgevine.github.com:wedgevine/tool.git
        # note the above hostname notation which shoud match what is defined in config file
1. Add key to ssh-agent, so don't have to input passphrase every time

        # start ssh agent
        eval "$(ssh-agent -s)"
        # check ssh keys added
        ssh-add -l
        # add ssh key
        ssh-add ~/.ssh/id_rsa_wedgevine
1. Since the key has been stored in ssh-agent, we can do normal Git add/commit/push


## Github pages
Any repo/organization/account could have a public facing static website at github.io per [^2]


## Github actions
Enable automatic software development workflow including CI/CD triggered by events such as "git push".

There are many pre-defined actions on Github marketplace, for example, for Hugo static site, [^3] can build
and deploy it to Github pages automatically.


[^1]: [How to manage multiple GitHub accounts on a single machine with SSH keys](https://www.freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/)
[^2]: [Types of GitHub Pages sites](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites)
[^3]: [Hugo setup](https://github.com/marketplace/actions/hugo-setup)

