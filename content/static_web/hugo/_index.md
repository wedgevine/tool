+++
title = "Hugo"
weight = 5
+++

## Install
```
mkdir ~/tools/hugo
wget https://github.com/gohugoio/hugo/releases/download/v0.62.2/hugo_0.62.2_Linux-64bit.deb
sudo dpkg -i hugo_0.62.2_Linux-64bit.deb
```

## Development
1. Local hugo repo setup

        ```
        hugo new site tool
        cd tool;
        # routine git initialization
        git init
        git config user.name "wedgevine"
        git config user.email "wedgevine@outlook.com"
        # add theme, see "Git Submodules basic explanation"
        git submodule add https://github.com/matcornic/hugo-theme-learn themes/hugo-theme-learn
        # add .gitignore
        cp ../know/.gitignore .
        # edit config.toml update base url, theme, etc
        # or copy existing content
        cp -R themes/book/exampleSite/content . prepare content or edit "_index.md"
        ```
2. Setting git remote url and adding key to ssh-agent, check {{< ref "/basic/git/github/#github-setup" >}}
3. Building Hugo site and deploying to Github Pages using Github actions

    Per[^1], for any Github repos, gh-pages branch can be used as a public facing website, the repo itself
    could be anything, a Hugo site, a react app[^2], as long as what in the gh-pages branch is a static website.
    Helped by Github actions CI/CD capability, we can setup workflow to automatically build and deploy Hugo
    site to a repo's gh-pages branch whenever we do "git push origin master"[^3]

        ```
        # generate keys for the repo
        ssh-keygen -t rsa -b 4096 -C "wedgevine@outlook.com" -f gh-pages-tool -N ""
        # copy pub key to repo tool - Settings - Deploy keys - Add deploy key, with name gh-pages-tool, allow write access
        # copy pub key to repo tool - Settings - Deploy keys - Add deploy key, with name gh-pages-tool, allow write access
        # create workflow file
        mkdir .github/workflow
        cd .github/workflow
        vi gh-pages.yml
        ```

        ```
        name: github pages

        on:
          push:
            branches:
            - master

        jobs:
          build-deploy:
            runs-on: ubuntu-18.04
            steps:
            - uses: actions/checkout@v1
              with:
                submodules: true

            - name: Setup Hugo
              uses: peaceiris/actions-hugo@v2
              with:
                hugo-version: '0.62.2'
                extended: true

            - name: Build
              run: hugo --minify

            - name: Deploy
              uses: peaceiris/actions-gh-pages@v2
              env:
                ACTIONS_DEPLOY_KEY: ${{ secrets.ACTIONS_DEPLOY_KEY }}
                PUBLISH_BRANCH: gh-pages
                PUBLISH_DIR: ./public

        ```


[^1]: {{< ref "/basic/git/github/#github-pages" >}}
[^2]: [a react app](https://medium.com/@Keithweaver_/setting-up-github-actions-for-a-react-app-on-github-pages-f66b28c312ac)
[^3]: {{< ref "/basic/git/github/#github-actions" >}}
