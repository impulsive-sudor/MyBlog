---
title: My domain in AWS with Terraform - Part 1 - Import
date: 2024-01-15T13:02:14.045Z
draft: false
featured_image: /images/895882_Managing an Amazon Route53 domain with the help of_xl-1024-v1-0.png
type: Article
keywords:
    - Amazon Route53
    - AWS
    - Domain
    - Fastmail
    - Infrastructure
    - Terraform
    - Email
slug: domain-aws-terraform-part-1-import
---

Currently, I have two domains setup in my AWS environment, one for personal and one for my family. I want the ability to manage these domains programmatically using [Terraform](https://www.terraform.io). This might be overkill for most people but I like to tinker with things. I'm hoping at the end of this process I can easily change my [Amazon Route53](https://aws.amazon.com/route53/) configuration while self documenting all the changes through GIT and CI/CD.

## Terraform Import

My AWS infrastructure was already setup using the console, so I need a way to turn that into code. Technically, I could just recreate everything but I thought, there has to be a better way. Then one day I heard about something called [Terraform Import](https://developer.hashicorp.com/terraform/cli/import). Basically, it's a way to target your current configurations using IDs with the ability to import it in your code.

There's a few ways to import your AWS infrastructure into Terraform, you can either use the CLI or write the code inside a tf file. Since I'm importing a handful of configurations, I decided on created a *import.tf* file and writting all my import code inside there.

This is what my *import.tf* file looks like:
> For the most up to date code, please use reference my [Github Repo](https://github.com/impulsive-sudor/TF-Import-AWS-Route53-Zone-and-Records/blob/main/import.tf).

```terraform
import {
  to = aws_route53_zone.zonefm
  id = var.zone_id
}

import {
  to = aws_route53_record.mx-1
  id = "${var.zone_id}_${var.my_domain}_MX"
}

import {
  to = aws_route53_record.soa-1
  id = "${var.zone_id}_${var.my_domain}_SOA"
}

import {
  to = aws_route53_record.txt-1
  id = "${var.zone_id}_${var.my_domain}_TXT"
}

import {
  to = aws_route53_record.ns-1
  id = "${var.zone_id}_${var.my_domain}_NS"
}

import {
  to = aws_route53_record.cname-1
  id = "${var.zone_id}_fm1${var.cname}_CNAME"
}

import {
  to = aws_route53_record.cname-2
  id = "${var.zone_id}_fm2${var.cname}_CNAME"
}

import {
  to = aws_route53_record.cname-3
  id = "${var.zone_id}_fm3${var.cname}_CNAME"
}
```

After all the import code is written, I run the command:

```zsh
terraform plan -generate-config-out=generated.tf
```

This will output my current configurations into a *generated.tf* file.

> Note: I couldn't figure out how to get one function for the import on CNAMEs. I tried doing a count with ```count.index``` but for some reason it was throwing up errors. If anyone has suggestions, please reach out.

During my import, I did notice some errors around "multivalue_answer_routing_policy". These errors do not stop the import of infrastructure but do require a change to the boolean values in your code.

> Note: For a easy fix, go into your generated.tf file and remove the "multivalue_answer_routing_policy = false" line. This is assuming you don't actually need multivalue routing policies.

## My code and how to use it

If you like to mirror what I did, you can [clone my repo](ttps://github.com/impulsive-sudor/TF-Import-AWS-Route53-Zone-and-Records/tree/main).

1. Clone the repo to your local machine

    ```zsh
    git clone "https://github.com/impulsive-sudor/TF-Import-AWS-Route53-Zone-and-Records.git"
    ```

2. Change the tfvar values in the *terraform.tfvars* file to ones that are relevant to your environment.

    ```terraform
    aws_region = "us-east-1"
    zone_id = ""
    my_domain = "example.com"
    cname = "._domainkey.example.com"
    ```

3. If you aren't using [Fastmail](https://www.fastmail.com), adjust the "fm" ID in the CNAME to what's used by your email provider. (For example, [Protonmail](https://proton.me/mail) is just "protonmail")

    ```terraform
    import {
    to = aws_route53_record.cname-1
    id = "${var.zone_id}_fm1${var.cname}_CNAME"
    }
    ```

4. Run the following command to initialize the directory.

    ```zsh
    terraform init
    ```

5. Run the following command to output your current infrastructure into terraform code.

    ```zsh
    terraform plan -generate-config-out=generated.tf
    ```

6. You should now see a *generated.tf* file in your current directory. If you do, congrats! You have successfully imported your Terraform infrastructure using Terraform import.
