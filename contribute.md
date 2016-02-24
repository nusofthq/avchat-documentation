---
layout: default
title: How to contribute to the documentation
description: Short tutorial on working with GitHub
isHome: false
hide: true
---

<div markdown="1">
<p class="lead">In this tutorial you will learn how to fork a GitHub repository and make changes that you can after commit in our documentation repository</p>

<h2>Create a GitHub account</h2>

First thing you will need to do is create a [GitHub](https://github.com/) account in case you don't have one.

Follow the steps and complete the sign up form as on any other site.

<h2>Forking the documentation</h2>

In the bottom of any page from the documentation, you will see the <kbd>Fork</kbd> button.

<img src="{{site.github.url}}/assets/images/fork.png" class="img-responsive" />

Click on it and you will be taken into your GitHub account or asked to sign up first if you are not already.

<img src="{{site.github.url}}/assets/images/where-fork.png" class="img-responsive" />

A copy of our main repository will be created in your account

<img src="{{site.github.url}}/assets/images/forked.png" class="img-responsive" />

Here you can edit any file related to **AVChat Standalone** or the **AVChat Integrations**


<h2>Editing the documentation files</h2>

The **AVChat Standalone** files are located inside the `_includes` folder and are named after every major chapter i.e. `design.md`, `features.md`, etc.

The **AVChat integration** files are located in the `root` of the repo and are named after the integration i.e. `drupal.md`, `joomla-3.md`, etc.

To edit it follow these steps:

1. Click on the file you wish to edit.
2. The file will open inside the browser. For this tutorial I've opened up `design.md`.
<img src="{{site.github.url}}/assets/images/edit-doc.png" class="img-responsive" />
3. Click on the <kbd>Edit</kbd> button showed in the image above.
4. Now you can edit any part of the file writing in Markdown (it is very simple, you can learn it by example with what is already written).
5. Select **Create a new branch for this commit and start a pull request.**
6. Make your changes and click <kbd>Propose file change</kbd>

<img src="{{site.github.url}}/assets/images/pull-request.png" class="img-responsive" />

We will be notified that a new pull request exists and after reviewing it we will accept the change and will be viewable in the main documentation.

</div>
