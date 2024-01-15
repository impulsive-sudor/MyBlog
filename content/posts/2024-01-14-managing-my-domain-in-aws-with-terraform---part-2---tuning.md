---
title: My domain in AWS with Terraform - Part 2 - Tuning
date: 2024-01-14T17:17:03.744Z
draft: true
featured_image: ""
type: ""
---


5. If you don't need multivalue routing (which if you don't know what this is, you most likely don't), remove all the lines of this in the generated.tf file. 
6. I recommend moving this code out of the generated.tf file and into the main.tf. When I did this, I also organized the code a bit so it made more sense (I prefer to have the Zone resources at the top of my code).
7. *Optional but recommended* replace any information in your code that should remain private. Your zone_id should be at least changed to var.zone_id to reference your ID in the tfvars file. If you are using the terraform.gitignore file, your tfvars file shouldn't get sent to your git repo on commit. If you are committing to a public repo, I advise hiding any [PII](https://en.wikipedia.org/wiki/Personal_data) in the public code. 
   1. Reference on gitignore for Terraform: <https://github.com/github/gitignore/blob/main/Terraform.gitignore>
8. Once all the code is in the main.tf file, you can delete the import.tf and generated.tf files

