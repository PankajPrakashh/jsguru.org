---
title: "Install NodeJS, Angular CLI, VSCode and Setup Angular Workspace Environment"
date: 2021-11-23T16:04:43+05:30
lastmod: 2021-11-23T16:04:43+05:30
draft: false

weight: 1
author: Pankaj Prakash
authorLink: https://jsguru.org
description: "In this article we will go through all the softwares and setup you require to create an Angular application. We will learn to install NodeJS, npm, yarn, Angular CLI and VSCode."
images: ["/images/angular/install-and-setup-environment/ng-version.png"]

tags: ["Angular", "Install", "Configure"]
categories: ["Angular"]
featuredImage: "/images/angular/install-and-setup-environment/ng-version.png"

lightgallery: true
---
Before we begin our journey with Angular, lets get equipped with all the required tools. In this article we will go through all the softwares and setup you require to create an Angular application.

<!-- more -->

To develop angular apps we must ensure our machine has NodeJS, npm or yarn, Angular CLI and an IDE or Code Editor.

## Install NodeJS
[NodeJS](https://nodejs.org/) is a JavaScript runtime environment. Angular uses it for several purposes e.g. 
1. [Transpiling](https://stackoverflow.com/a/44932758/2401088) TypeScript to JavaScript, SCSS to CSS, SASS to CSS etc.
2. Building and packing final JS sources.
3. Provide runtime environment for angular to run.

To install nodejs hit over [nodejs downloads section](https://nodejs.org/en/download/) and select appropriate download bundle for your operating system. Post download and installation open terminal and run command `node -v` to verify nodejs installed version.

###  Install Node Package Manager (Npm or Yarn)
Once you have installed nodejs, you require a package manager to install/uninstall other JS libraries. Node ships with "_npm_" as its default package manager. To check the npm version open terminal and hit `npm -v`.

I would recommend to install Yarn (Yet Another Resource Negotiator) as your package manager. To install yarn open terminal and hit `npm install --global yarn`. Once the installation completes execute `yarn -v` to check the installed version.

## Install Angular CLI
Angular CLI is a set of command line tools we will be using to create, run, test and build our angular app. After you have installed nodejs, npm or yarn let's install angular. Open terminal and hit `npm install -g @angular/cli` or `yarn global add @angular/cli`. 

Once the installation is complete hit `ng --version` to verify the installed version.


![ng --version](/images/angular/install-and-setup-environment/ng-version.png "ng --version console output")

## Install VSCode
Finally we have all the necessary softwares installed on our machine. At last we need a code editor. You are free to choose any code editors or IDE of your choice. I would recommend VSCode for two primary reasons - 

1. Its open source - free to use.
2. Powerful and lightweight.

To download VSCode navigate to [VSCode downloads section](https://code.visualstudio.com/download) and download required setup based on your operating system. 

![Visual Studio Code](/images/angular/install-and-setup-environment/vs-code.png "Visual Studio Code")

👏 All set, we are all good to create our first angular application.
 
&nbsp;  
Happy Coding :man_technologist: