---
title: Setting up Netlify CMS on Hugo
date: 2018-01-26T10:16:54.728Z
draft: false
categories:
  - Tutorials
  - Netlify
tags:
  - Netlify
  - NetlifyCMS
  - Hugo
keywords:
  - Netlify
  - NetlifyCMS
  - Hugo
  - Setting up Netlify CMS on Hugo
  - Static website generator Netlify
  - Host static blog on Netlify
autoThumbnailImage: false
thumbnailImagePosition: ''
---
# About [Netlify CMS](https://www.netlifycms.org/):

> Netlify CMS is an open source content management system for your Git workflow that enables you to provide editors with friendly UI and intuitive workflow. You can use it with any static site generator to create faster, more flexible web projects. Content is stored in your Git repository alongside your code for easier versioning, multi-channel publishing, and the option to handle content updates directly in Git.

# Installing and configuring Netlify CMS:

In this guide I am going to show you how to setup Netlify CMS on a Hugo based site. The **prerequisites **for the next steps are:

* A Hugo website/blog
* GitHub account and basic usage
* A Netlify Account

## Step 1. Creating the admin files

All Netlify CMS files are contained in a static admin folder, stored at the root of your published site. The static files of a Hugo site are stored inside the `/static` location at the root of your website. 

Navigate to `static` of your website and create a folder named `admin` inside it. If there is no `static` folder in your website then simply create a new folder and name it. 

The `admin` folder of Netlify CMS contains two files: 

admin

├ index.html

└ config.yml

Let us first create the file `index.html` inside the admin folder The content of this file will be:

```
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Content Manager</title>

  <!-- Include the styles for the Netlify CMS UI, after your own styles -->
  <link rel="stylesheet" href="https://unpkg.com/netlify-cms@^1.0.0/dist/cms.css" />

</head>
<body>
  <!-- Include the script that builds the page and powers Netlify CMS -->
  <script src="https://unpkg.com/netlify-cms@^1.0.0/dist/cms.js"></script>
</body>
</html>
```

This file allows us to access the admin panel for our website. You will be accessing your admin panel at `yourwebsite.com/admin` . This file loads up the required script and CSS for Netlify CMS.

In the next file we will configure our Netlify CMS installation. Create a file named `config.yml` at `/static/admin` and proceed to the next step.

## Step 2. Configuring config.yml file
{{< gist ragasirtahk 9f70fb00d5cf8c94c175a0a4fb9ba553 >}}
