# ACME Corporation

Exercise from the book *Hugo in Action - Static sites and dynamic Jamstack apps* by Atishay Jain.

It is currently (25/09/2021) still a MEAP, *Manning Early Access Program*, and at version 12.

Restarting on 2021-11-22 with version 13.

Create the site:

```bash
hugo new site acme_corp --format yaml
```

**YAML**: YAML Ain't Markup Language

**TOML**: Tom's Obvious Minimal Language

**!!!**: The items in the numbered list at the beginning of chapter 2.2 all have the number 1.

**!!!**: Exercise 2.5 should be moved from before chapter 2.3.1 to before chapter 2.3

**!!!**: The items in the numbered list in chapter 2.4.2 all have the number 1.

I am not interested in **Netlify** hosting (chapter 2.4.1) and after reading chapter 2.4.2 on **GitHub** Pages twice I still have no idea how to do it.

With the help of [GitHub Action Hugo setup](https://github.com/marketplace/actions/hugo-setup), [GitHub Actions for GitHub Pages](https://github.com/peaceiris/actions-gh-pages), and [Hugo - Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/) I did manage to create a project page at [https://jmares.github.io/acme_corp/](https://jmares.github.io/acme_corp/).

In the `config.yaml`:

```yaml
baseURL: https://jmares.github.io/acme_corp/
```

The complete `gh-pages.yaml`:

```yaml
name: GitHub Pages

on:
  push:
    branches:
      - main  # Set a branch name to trigger deployment
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: ${{ github.ref == 'refs/heads/main' }}
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

It isn't always clear for example if a file needs to be put in the main `static` folder or the theme's `static` folder.

**It is strongly advised to minimize the use of embedded HTML in Markdown content.**

Inline HTML is disabled by default in Hugo and needs to be enabled using the config.

```yaml
markup:
  goldmark:
    renderer:
      unsafe: true
```

Have I encoutered even one subchapter from the chapters 3 and 4 without errors?

Chapter 4.4 and before: In the text the author uses floats (eg. 1.2) for the weights, but in the sample code he uses integers (eg. 120).

I AM NEVER GOING TO BUY A MEAP (Manning Early Access Program) BOOK AGAIN. 

Instead of feeling privileged for having early access, what I feel is frustration of having to work with an unfinished book.

I wish I had never started with this book. Chapter 5 was slightly better, but chapter 6 is chaotic. Sometimes it doesn't mention the files you need to copy to your site, then you get a snippet of code, but nowhere is mentioned where in the given file it belongs, so you have to look it up in GitHub repository for this book. Most frustratingly is when you have to add a snippet of code, but it is nowhere to be found on the GitHub repository. Or the code in the GitHub repository doens't match the code from the book. I already came very close just forgot about this book.

A couple of pages later: I quit. I barely know what I am doing, the text in the book doens't give me an understanding of hwat I am doing and why.

