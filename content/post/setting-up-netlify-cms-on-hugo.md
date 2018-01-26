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

In this guide I am going to show you how to setup Netlify CMS on a Hugo based site. We will be hosting the website on GitHub and Netlify. The **prerequisites **for the next steps are:

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

This file allows us to access the admin panel for our website. You will be accessing your admin panel at `yourwebsite.com/admin`. This file loads up the required script and CSS for Netlify CMS.

In the next file we will configure our Netlify CMS installation. Create a file named `config.yml` at `/static/admin` and proceed to the next step.

## Step 2. Configuring config.yml file

Configuring this file depends a lot on your site. The common configurations for each website are described below. Since **we are using Netlify and GitHub for hosting** our website so enter this in your file:

```
backend:   name: git-gateway  branch: master # Branch to update (optional; defaults to master)
```

You have the option to **enable the Editorial Workflow**, which adds an interface for drafting, reviewing, and approving posts. To do this, add the following line to your `config.yml`:

```
publish_mode: editorial_workflow
```

Next we are going to specify the locations where Netlify CMS will store the images you upload to your blog. I wish to store the files in `static/images/uploads` folder of my website and make them available in the published website at `/images/uploads`.

While `media_folder` specifies where uploaded files will be saved in the repo, `public_folder` indicates where they can be found in the published site. Depending upon your requirements you may edit the code:

```
media_folder: "static/images/uploads" # Media files will be stored in the repo under static/images/uploadspublic_folder: "/images/uploads" # The src attribute for uploaded media will begin with /images/uploads
```

_Note: If `public_folder` is not set, Netlify CMS will default to the same value as `media_folder`, adding an opening / if one is not included. _

**Next comes the tricky part of the configurations....**

Collections define the structure for the different content types on your static site. Since every site is different, the `collections` settings will be very different from one site to the next.

I wanted my website to have these options while creating a post: `Title, Publish Date, Draft, Categories, Tags, Keywords, Auto Thumbnail Image Option, Thumbnail Image, Cover Image and Body`. If you wish to have the same for your website then proceed further otherwise visit the Netlify CMS docs for `Collections` on [this link](https://www.netlifycms.org/docs/add-to-your-site/#collections).

Enter these lines to your code in the `config.yml` file:

```
collections:

  - name: "posts" # Used in routes, e.g., /admin/collections/blog

    label: "Post" # Used in the UI

    folder: "content/post" # The path to the folder where the documents are stored

    create: true # Allow users to create new documents in this collection

    slug: "{{slug}}" # Filename template, e.g., YYYY-MM-DD-title.md

    fields: # The fields for each document, usually in front matter

      - label: "Title"
        name: "title"
        widget: "string"

      - label: "Publish Date"
        name: "date"
        required: false
        widget: "datetime"

      - label: "Draft"
        name: "draft"
        required: false
        widget: "boolean"
        default: true

      - label: "Categories"
        name: "categories"
        required: false
        widget: "list"

      - label: "Tags"
        name: "tags"
        required: false
        widget: "list"

      - label: "Keywords"
        name: "keywords"
        required: false
        widget: "list"

      - label: "Auto Thumbnail Image"
        name: "autoThumbnailImage"
        required: false
        widget: "boolean"
        default: true

      - label: "Thumbnail Image Position"
        name: "thumbnailImagePosition"
        required: false
        widget: "select"
        options: ["left", "top", "right"]

      - label: "Thumbnail Image"
        name: "thumbnailImage"
        required: false
        widget: "image"

      - label: "Cover Image"
        name: "coverImage"
        required: false
        widget: "image"

      - label: "Body"
        name: "body"
        widget: "markdown"
```
