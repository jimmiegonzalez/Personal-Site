---
title: ":mailbox: What is Postman? And how to get started"
layout: post
date: 2022-01-24 22:10
tag: [Postman, How-to Guide]
#image: https://sergiokopplin.github.io/indigo/assets/images/jekyll-logo-light-solid.png
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "This how-to guide was created for students at Thinkful in order to set up and use the API platform tool Postman."
category: project
author: jimmiegonzalez
externalLink: false
---

![Postman Logo](/assets/images/postman.png "Postman Logo")

# Introduction

Postman is a popular API client that makes it easy for developers to not only share APIs, but create, test, and document APIs as well. This is done by allowing users to create and save both simple and complex HTTP requests, as well as read the responses. This results in more efficient and less tedious work for developers.

# Getting Started

To start, first download [Postman](https://www.postman.com/).

![Sign up page](/assets/postman/Postman-download.png "Home page")

You will then be directed to the download page. Although there is a web version of Postman, downloading the desktop app is highly recommended as it allows you to access all features.

![Download page](/assets/postman/postman-download-page.png "Download page")

# Application Overview

Once Postman is installed, you will see something similar to this page:

![Application Overview](/assets/postman/application-overview-edited.png "Application Overview")

Take note of the following components labeled in the image above:

1. The navigation bar at the top of Postman allows you to switch workspaces and
   includes the New button.
2. The sidebar allows you to filter historical requests that you’ve made. It also lets you
   create new collections for your requests.
3. The main section of the application will be where you see the requests that you
   make. The app typically starts up on the Launchpad screen. The New tab ➕ icon
   allows you to start a new request.

# Customization

By selecting the various dividers and closing tabs, you can simplify your workflow. Click
the New tab button in the main section of the page and then follow the instructions below
to create a more streamlined view.

1. Close the Launchpad tab.
2. Open a new request tab by clicking the New tab button.
3. Drag the sidebar divider to the left to collapse the sidebar.
4. Drag the Response section of the new request tab up to hide the Params section.

Your page should look something like this when you're done:

![Customization](/assets/postman/customization.png "Customization")

# Making Your First Request

To make a request with Postman, type a URL like [https://dev.to/](https://dev.to/). into the location bar that’s
next to the drop-down menu with the word **GET** in it, as shown below. Then, click **Send**.

![GET request](/assets/postman/GET-request.png "GET request")

The response section will change to include a number of tabs, including the Body tab. In it,
you’ll see both HTML and CSS!

By default, Postman will suggest that you save your requests in case you end up using
them often. You don’t have to save your request in this instance.

You can click the **Preview** button that is within the **Body** section. Although it may not look
exactly the same, you will probably recognize some elements from the Dev.to website.

# Conclusion

At its most basic, Postman is a software application that allows you to make web requests
without the use of a browser. However, after exploring more of its features, you will
quickly notice that Postman can do much more than make requests and inspect results.
