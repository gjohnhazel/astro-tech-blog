---
title: 'The Era of AI Agents'
description: "The Era of AI Agents is upon us and I'm here for it"
pubDate: 'March 6 2025'
# heroImage: 
#   src: '/blog-placeholder-5.jpg'
#   alt: 'blog placeholder'
tags: ["journal"]
updatedDate: 'March 6 2025'
series: "journal"
---

About 4 months ago I caught wind of Replit's new Replit AI feature and began using it's Agentic AI to build applications. I was blown away. Despite what folks on Reddit will have you believe, it's pretty dang good. People complain because they want it to be perfect right out the gate. HELLO- human programmers don't even build applications without trial and error.

Anyway, I've built and deployed several apps on Replit with the AI Agent over the last few months and have loved it.

But I'm excited because today I took Agentic work to the next level.

A few months ago (looks like maybe late November, 2024), Cursor released an Agent mode. I've been using Cursor since late 2023, but had not been compelled to sign up for their paid plan until this (and yes, I know you can bring your own API keys from the AI companies, which I did have plugged in, but it eats through credits so fast that way).

Having the Agent build my application was pretty cool once I put it in yolo mode (I know, I know, letting AI control my computer while being barely supervised is scary, but it freakin' works!)

But when it came time to deploy, the process was going much slower. I was trying to deploy to an existing server alongside several other similar-purposed applications but I wanted a clean CI/CD pipeline, so I was having the agent do most of the server config in the GitHub action / deploy.yml.
But this was getting annoying as we, of course, kept running into errors.

Finally I realized... if it can control my CLI then I can put it in charge of the whole pipeline.
Originally, it thought it couldn't do it, so I reminded it that it can run commands on my computer. I told it to use git cli and commit & push, then use gh cli to monitor the gh action, and then to ssh into my server and gave it the command for that.
Boom.
Now it's using trial and error, discovering & resolving its own mistakes, all while I write this blog post. And soon, the application will be deployed.

It's rudimentary right now, but it works. I'm excited to see where agentic AI takes us in 2025, and even more excited for 2026.