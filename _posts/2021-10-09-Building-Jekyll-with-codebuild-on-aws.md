---
title: Building Jekyll with codebuild on AWS
author: Bruno Russo
date: 2021-10-09 22:00 0300
categories: [Cloud, AWS, CodeBuild, Jekyll]
tags: [AWS, Cloud]
layout: post
type: post
---

An example of CodeBuild to build a static site by Jekyll.

## Architecture

![Architecture](https://brunorusso.com.br/assets/Archtecture-jekyll-codedeploy.png)

## Resources AWS used in this deploy:

* CodeCommit
* CodeBuild
* CodePipeline
* S3


## buildspec.yml

```yml
version: 0.1
   
phases:
  install:
    commands:
      - apt-get update
      - apt-get install build-essential 
      - apt-get install zlib1g-dev
      - gem install jekyll:4.2.0
      - gem install rouge:3.26.0
      - gem install bundler
  build:
    commands:
      - echo "******** Building Jekyll site ********"
      - jekyll build
artifacts:
  files:
    - '**/*'
  base-directory: '_site'
```
