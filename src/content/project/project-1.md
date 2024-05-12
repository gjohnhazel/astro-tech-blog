---
title: 'Obsidian as a CMS'
description: 'Setting up an Astro Blog with Obsidian as a CMS'
pubDate: 'May 10 2024'
heroImage:
    url: '/blog-placeholder-about.jpg'
    alt: 'GitHub wallpaper'
platform: Web
stack: ['vscode-icons:file-type-astro', 'vscode-icons:file-type-js', 'logos:vercel-icon', 'simple-icons:obsidian']
website: https://portfolio.johnhazel.com
github: https://github.com/gjohnhazel/astro-blog
order: 2
---

My own personal blog, with Obsidian as a CMS.

The concept intrigued me because I wanted to make blogging so enjoyable & accessible for myself that I would be drawn to do it and take joy in it.

It seemed simple enough of a concept. But the big challenge for me was that this was basically my first adventure into a serverless environment.

So my original code was built from a server-mindset and it took a good bit of perspective shifting to make it work for Vercel.

Anyway, it works now! Basically looks like:
Obsidian > github/obsidian > github/astro-blog > vercel
1. Use Obsidian Git Plugin to commit & push when a new Blog Post is up
2. gjohnhazel/obsidian repo (private) receives the push and triggers a GitHub action to trigger [this GitHub action](https://github.com/gjohnhazel/astro-blog/blob/main/.github/workflows/update_blog.yml) in gjohnhazel/astro-blog.
3. The GitHub action deploys to Vercel
4. Vercel's Build script calls on [fetchContent.js](https://github.com/gjohnhazel/astro-blog/blob/main/fetchContent.js) which pulls the content from the Obsidian repo, does any transformations needed, and saves the images
5. The build script finishes and the site is re-deployed with the updated content!

To re-create this:
1. Fork or clone [this repo](https://github.com/gjohnhazel/astro-blog)
2. In Obsidian, install [this Obsidian git plugin](https://github.com/denolehov/obsidian-git)
3. Create the following GitHub action in your repo (obsidian/.github/workflows/main.yml)

```
    name: Sync Blog from Obsidian to Astro Blog

    on:
    push:
        paths:
        - 'Blog/**'
    repository_dispatch:
        types: [simulate_push]

    jobs:
    trigger:
        runs-on: ubuntu-latest
        steps:
        - name: Repository Dispatch
        uses: peter-evans/repository-dispatch@v1
        with:
            token: ${{ secrets.REPO_DISPATCH_TOKEN }}
            repository: gjohnhazel/astro-blog
            event-type: update-blog  # This should match the type expected by the receiving repo's workflow
```

4. Create the following Secrets in your Repos under repo > Settings > Secrets and variables > Actions:
    a. In Obsidian repo, REPO_DISPATCH_TOKEN
    b. In astro-blog repo, TEABLE_API_KEY (if you take advantage of categories & Teable), VERCEL_PROJECT_ID, VERCEL_TOKEN
