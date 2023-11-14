+++
title = "Deploying My Blog"
date = "2023-11-12T17:26:22.854Z"
draft = true
featured_image = "/images/DALL·E 2023-11-12 12.23.20 - A fantasy-themed, vivid image featuring anthropomorphic characters representing Hugo and GitHub. Hugo is depicted as a wise, elderly wizard with a lon.png"
+++

# How to Deploy?

## Current Tool
The blog tool I'm using is called `Hugo`. I don't have much experience with it but I'm fan a fan of it's ability to easily translate markdown to HTML. Using Markdown is more universal and can be carried over to other platforms easily. 

## Git
To start, I want to use some kind of Git server to store and deploy my code. I'm not sure if it matters that this platform is private or public. 

## S3 Directly?
I have a few years of AWS experience, so I'm most likely going to put this in AWS. Since this is going to be a static site, the costs should be minimal. I could deploy this site directly to a S3 bucket but I'd rather use CI/CD to deploy. 

## What I ended up deploying
I ended up deploying this blog using Github pages due to how easy and cost effective it is to do. As of writting this post, there's no cost to setting up Github pages on a public repo. 

## Steps I took
1. First I created my Hugo page locally on my mac by following the steps on Hugos [quickstart](https://gohugo.io/getting-started/quick-start/) site
2. Then I followed the guide on how to [deploy using Github Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/).
3. After following those two guides, I was able to deploy my first Blog.

## Pictures
I needed a way to add pcitures to my posts. Without pictues, I feel the blog is less interesting. So to make my life easy, I decided on paying for the openai service that allows me to use DALL-E 3 image generation. 