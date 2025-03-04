# Blog

A flower tech blog for sharing knowledge!

**[Link to blog](https://krafthem.github.io/blog/)**

## stack

This is a blog setup using [Hugo](https://gohugo.io/), which is a open source framework for SSG. The blog is hosted on [Github Pages](https://pages.github.com/).

### configuration

#### github actions

Github actions is used to deploy the blog. We use whats written in this [guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

#### theme

For theme we are using [Hugo blog awesome](https://themes.gohugo.io/themes/hugo-blog-awesome/). The theme is install as a git submodule

To be able to allow setting author on posts I have overwritten the post theme post [layout](https://github.com/hugo-sid/hugo-blog-awesome/blob/c4a6784e1784c160355cafbde149e41ab14f6b0b/layouts/_default/single.html) with a [copy](https://github.com/Krafthem/blog/blob/main/layouts/_default/single.html) that allows setting author.

## how to blog

First install hugo ([install guides](https://gohugo.io/installation/))

Then make a new post by running:

    hugo new posts/my-new-post.md

To serve the blog run:

    hugo server -D

(the -D serves drafts, see the params in you blog post)

To build you can run

    hugo build

Voila! blog away!

To deploy blog, just merge to main!
