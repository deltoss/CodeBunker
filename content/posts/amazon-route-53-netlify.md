---
title: Redirecting Amazon Route 53 to Netlify Site
subtitle: Using AWS with Netlify
category:
  - AWS
author: Michael Tran
date: 2020-10-03T08:44:09.436Z
featureImage: /uploads/512px-amazon_web_services_logo.png
---
I've made a blog with [Netlify CMS](https://www.netlifycms.org/docs/start-with-a-template/) because it was free, simple & easy to set up. When I created my blog via Netlify, it provided me with a free subdomain to reach my site, in the format of `*.netlify.app`.

I've recently completed the ([Developers Associate](https://aws.amazon.com/certification/certified-developer-associate/)) AWS certification. As part of it, I bought a domain via [Amazon Route 53](https://aws.amazon.com/route53/) so that I could fiddle & learn how to use `Amazon Route 53`.

I already had a domain registered with `Amazon Route 53`, but now that I've finished my certification, the domain is just sitting there, collecting dust... I figured why don't I have my `Netlify` blog use it?

So I began my journey and went onto the path of fiddling with both `Netlify` and `Amazon Route 53`. I had success with a bit of trial and error, so thought it's a good idea to share how I've done it.

<!-- omit in toc -->

## Table of Contents

* [Pre-requisites](#pre-requisites)
* [Instructions](#instructions)

  * [Netlify Adjustments](#netlify-adjustments)
  * [Adding Records to Amazon Route 53](#adding-records-to-amazon-route-53)
* [Additional Information](#additional-information)

## Pre-requisites

These instructions assumes you've already:

1. Created your `Netlify` site.
2. Bought a AWS Route 53 domain.

## Instructions

I've created `Netlify` blog site with the `Netlify` domain of `codebunker.netlify.app`. The goal here is to use a domain which was registered via `Amazon Route 53` and assign it to the `Netlify` blog site.

For example, the main domain I've bought from `Amazon Route 53` is `codebunker.com.au`. Using the below instructions, I've set up `Netlify` & `Amazon Route 53` in such a way where the below subdomains can be used to access the Netlify site:

* `blog.codebunker.com.au`
* `www.blog.codebunker.com.au`

### Netlify Adjustments

We'll make configuration adjustments on our `Netlify` site:

1. Login to your Netlify dashboard via <https://app.netlify.com/>.
2. Navigate to domain settings for the site you want to configure the domain for.

   ![Netlify - Navigate to Domain Management](/uploads/netlify-navigate-to-domain-management.gif "Netlify - Navigate to Domain Management")
3. From the `Domain Management` page, add your primary domain & any number of [domain aliases](https://docs.netlify.com/domains-https/custom-domains/#definitions). See the below GIF.

   ![Netlify - Adding Domain & Domain Aliases](/uploads/netlify-adding-domain-domain-aliases.gif "Netlify - Adding Domain & Domain Aliases")
4. Now you need to set up the `Netlify DNS` for your primary domain. See the below GIF.

   ![Netlify - Setting up Netlify DNS](/uploads/netlify-setting-up-netlify-dns.gif "Netlify - Setting up Netlify DNS")

### Adding Records to Amazon Route 53

If you haven't registered a domain, see [Register a Domain Name with Amazon Route 53](https://aws.amazon.com/getting-started/hands-on/get-a-domain/).

After registering a domain with Amazon Route 53, you need to create the hosted zone for it.For more information, see [Creating a public hosted zone](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/CreatingHostedZone.html).

Once you've completed the above pre-requisites, follow the below steps:

1. Login into [AWS console](https://console.aws.amazon.com/console/home?nc2=h_ct&src=header-signin).
2. Navigate to the `Amazon Route 53` service.

   ![Amazon Route 53 - Navigate to Amazon Route 53 Service](/uploads/amazon-route-53-navigate-to-amazon-route-53.gif "Amazon Route 53 - Navigate to Amazon Route 53 Service")
3. Navigate to the `Hosted zones` tab and go into your hosted zone for your registered domain. Click on `Create record` to create your `CNAME` DNS record(s) that'd point to your Netlify website URL.

   The below GIF shows this process:

   ![Amazon Route 53 - Creating CNAME DNS Records](/uploads/amazon-route-53-creating-cname-dns-records.gif "Amazon Route 53 - Creating CNAME DNS Records")

   > Developer Tip 💡
   >
   > You can create as many DNS records as you want, as long as it's also configured on Netlify, and it's using your top level domain you've bought.
   >
   > Developer Tip 💡
   >
   > The Netlify Website URL can be found on your Netlify site dashboard. It's the URL assigned to your netlify app when it's created under the format of `*.netlify.app`).
   >
   > ![Netlify - Site Default Url](/uploads/netlify-site-default-url.jpg "Netlify - Site Default Url")

   You should end up with something like this:

   ![Amazon Route 53 - DNS Entries Results](/uploads/amazon-route-53-dns-entries-results.jpg "Amazon Route 53 - DNS Entries Results")
4. If you configured everything correctly, the DNS configurations should propagate within up-to 24 hours. Try hitting your website URL and confirm it works.

   ![Amazon Route 53 - Verifying the DNS Record Works](/uploads/amazon-route-53-verifying-the-dns-record-works.jpg "Amazon Route 53 - Verifying the DNS Record Works")

## Additional Information

* [Custom domains - Assign a domain to a site](https://docs.netlify.com/domains-https/custom-domains/#assign-a-domain-to-a-site)
* [Custom domains - Configure external DNS for a custom domain](https://docs.netlify.com/domains-https/custom-domains/configure-external-dns)