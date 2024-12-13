---
title: Cloud Start
author: Bruno Russo
date: 2021-11-08 12:45 0300
categories: [Cloud, AWS]
tags: [AWS, Cloud, Web, Arquitetura, Cloud Start, Terraform, Cloudformation]
layout: post
type: post
---

## About Cloud Start

Last week I started a new personal project called Cloud Start.

Cloud Start is a repository in GITHUB open to everyone can contribute.

The main objective of Cloud Start is to share examples of code to build infrastructure from “zero to hero”, starting from VPC and after deploying other services until having a three tier application running. 

I believe in a few weeks I will have finished the architecture of this application to share it. Of course, the architecture is live then changes can occur.   


At the moment I finished some scripts:

- Terraform
	- S3 to static website
	- EC2 with userdata, to automate first launch 
	- EC2 launch configuration
- Cloudformation
	- Create dynamoDB table
	- Create a VPC, Subnets, routing tables, Internet Gateway and NatGateway

There are other scripts under construction like an architecture.

All codes were written in Cloudformation and Terraform and in this first moment only deploy resources in AWS. In the future, I wish adjust the code of scripts to deploy in other clouds.

For more information visit: [https://github.com/brunorusso/cloud-start](https://github.com/brunorusso/cloud-start)
