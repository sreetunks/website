---
title:  "Setting up a Static Site with Jekyll"
date:   2020-06-19 23:40:00 +0530
categories: General
tags: [jekyll, azure, static-site]
---
Since this is the first post since moving the site to use Jekyll, I'll talk a little about the decision and some alternatives.

Recently a lot of people I know have been writing blog posts or setting up personal websites to do Game Design related writeups. A lot of them use popular WYSIWIG webpage creators like Wix or something like WordPress to set up their websites.
I'd been thinking of doing the same for a while but I'd never find the time to extend my website. But now I've finally moved my personal blog from a shared hosting provider to Azure and also started using Jekyll to generate my website for me.
A post on deciding to go with Jekyll and also mentioning some other similar tools and services that I didn't end up using seemed like a good place to start.

## Static Site Generators
---
Working with CSS is something I really don't enjoy. So when I was thinking of making a personal blog, I knew I had to find some way to avoid handling all the web page styling myself. I also wanted to commit myself to write frequent posts which would mean adding new HTML files, ensuring all the pages are connected and linked and that they share a consistent layout with each other. So I looked for tools other people were using these days to manage their blogs and found out about Static Site Generators.
Static Site Generators, in a simple sense, are parsers. They take lightly formatted text files as input and create full-fledged websites according to templates you specify with consistent theming and good page navigation. A lot of them use Markdown files and simple templating languages that allow you customize the layouts and theme of the generated webpages.
Adding a new post to the blog is done by creating a new Markdown file. The pages are automatically linked and themed and can also be automatically indexed in a 'Recent Posts' or 'Table of Contents' format.

Some popular Static Site Generators are:
- [Jekyll](https://jekyllrb.com/): Used by GitHub Pages as well. Uses Liquid for templating and Ruby Gems to generate the site.
- [Hugo](https://gohugo.io): Boasts very fast site build times, letting you instantly preview and iterate on your website's design. Uses Go for templating.

I decided to go with Jekyll since I already had a local Ruby environment set up. Jekyll targets blogs in particular with a lot more functionality geared towards maintaining a site with many articles and pages.   

## Hosting Services
---
There are quite a few options to host a Static Site for cheap in 2020. My final decision was to use Azure since I was already using some of their other services but I'll go over some of the other options I considered as well.

### <u>Shared hosting providers</u>
Before using Jekyll, I'd already had a single-page portfolio website that I had up and running. I was using a Shared hosting solution with a cPanel interface. For solutions like this, depending on your provider, you can either set up an FTP upload which copies the web page files generated on your computer to the server or set up a Git repository to which you can push the generated files.

### <u>Cloud-based storage</u>
Cloud Platforms like Amazon, Microsoft Azure and Google CLoud Platform offer products to host Static Sites. A lot of these Platforms also have additional features like CI/CD Pipeline integration which really helps simplify the workflow for getting a new blog post out. Some of them also have free trials where they give you access to their services for up to a year.

### <u>GitHub Pages</u>
This one, I was very surprised to hear about because it sounded way too good to be legitimate. GitHub offers, for every User/Project a `github.io` subdomain that they can use to host a webpage. The web page files are stored as a public/private GitHub repo with the only condition being that the website is not used for specific commercial purposes. Another feature of this is that it has built-in support for Jekyll, which means that instead of pushing the HTML files to the repo, you can push up your Jekyll files and the site gets built for you on GitHub's servers.

## Conclusion
---

As I'm typing this out, I'm pretty sure no one's ever making it this far down this post. This one's overly technical for not a lot of good reasons and is pretty much a throwaway post for me to get used to this whole thing. If you did come this far, yikes.

My next post will be the start of a series on Fighting Game Design where I explore archetypes present in contemporary fighting games and examine their canonicity and try to derive extensions from them to see if we can add something new to the popular genre.
