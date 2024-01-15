---
title: My domain in AWS with Terraform - Part 1 - Import
date: 2024-01-14T14:18:08.124Z
draft: true
featured_image: ""
type: ""
---

## Summary

Currently, I have two domains setup in my AWS environment, one for personal and my family. I want the ability to manage these domains progamitically using Terraform. I plan on doing this using Terraform Import.

## Terraform Import

Since I already have AWS infra setup the way I want, I need to import that into my terraform code. Technically, I could just recreate everything but I wanted to learn how to use the import function. 

There's a few ways to import your AWS Infra into Terraform, I've choosen using a import.tf file and putting all my code into that.

Once all the import code is written, I run the command:

```zsh
terraform plan -generate-config-out=generated.tf
```

This will output my current configurations into a *generated.tf* file. 

Note: I couldn't figure out how to have one function for the import on cnames. I tried doing a count with count.index but for some reason it was throwing up errors. If anyone has suggestions, please reach out.

During my import, I did notice some errors around "multivalue_answer_routing_policy". These errors do not stop the import of your infrasutrcte but do require you to change the boolean values in your code.

* to fix this, go into your generated.tf file and remove the "multivalue_answer_routing_policy = false" line.

## How to use this repo

If you like to mirrior what I did, you can clone my repo here <https://github.com/impulsive-sudor/TF-Import-AWS-Route53-Zone-and-Records/tree/main>

1. Clone the repo to your local machine

```zsh
git clone "https://github.com/impulsive-sudor/TF-Import-AWS-Route53-Zone-and-Records.git"
```

1. Change the tfvar values to ones that's relevant to your infrastructe.
2. If you aren't using Fastmail, adjust the "fm" ID code to what's used by your email provider. (For example, protonmail is just "protonmail")
3. Run the command ```zsh terraform plan -generate-config-out=generated.tf``` to output your current infrastructure into terraform code.

