---
title: My domain in AWS with Terraform - Part 3 - Deploy
date: 2024-01-14T17:17:28.186Z
draft: true
featured_image: ""
type: ""
---

9. Now for the moment of truth, run the command ```zsh terraform plan```. This will show you what exactly is being done, please note that if it says "add", that means it's adding resources, not changing what you currently have. 
10. Lastly, run ```zsh terraform deploy``` to deploy this infrastructure into the AWS account 
11. *Optional* Delete the previous hosted zone in AWS