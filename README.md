# Blog

A flower tech blog for sharing knowledge!

## stack

This is a blog setup using [Hugo](https://gohugo.io/), which is a open source framework for SSG. The blog is hosted on [Github Pages](https://pages.github.com/).

### configuration

#### github actions

Github actions is used to deploy the blog. We use whats written in this [guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

#### theme

For theme we are using [Hugo blog awesome](https://themes.gohugo.io/themes/hugo-blog-awesome/).

To be able to allow setting author on posts I have overwritten the post theme post [layout](themes/hugo-blog-awesome/layouts/_default/single.html) with a [copy](layouts/_default/single.html) that allows setting author.

## how to blog

First install hugo ([install guides](https://gohugo.io/installation/))

Then make a new post by running:

    `hugo new posts/my-new-post.md`

Voila! blog away!

To deploy blog, just merge to main!
