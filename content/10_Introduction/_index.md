---
title: "Introduction" 
chapter: true
weight: 10
---

## Learning Objectives

Today we will going to work through the following topics

- How to configure and use a community provided Relay workflow
- How to configure the Puppet Enterprise integration for Relay
- How infrastructure as code can enable further automation
- How combining Puppet Enterprise and Relay can facilitate policy enforcement

## Workshop Structure

The workshop covers the following topics and it is estimated that 1 to 1.5 hours will be required to complete.

- Prerequisites (10 minutes)
  - Create a Relay account
  - Provision Puppet Enterprise from the AWS Marketplace
  - Provision AWS IAM credentials with access to EC2
  - Provision one CentOS EC2 instances to the same region where you deploy Puppet Enterprise
- Setup (20 minutes)
  - Configure Relay workflow
  - Configure Puppet Enterprise
- Workshop Exercise (30 minutes)
  - Deploy EC2 instance and onboard into Puppet Enterprise
  - Manage sudo using infrastructure as code
  - Make an unauthorized change to sudo
  - Observe how Relay reacts to changes

{{% notice warning %}}
<p style='text-align: left;'>
The examples and sample code provided in this workshop are intended to be consumed as instructional content. These will help you understand how Puppet Enterprise, Relay, and AWS EC2 can be integrated together to build solutions which solve organizational challenges. These examples are not intended for used in production environments.
</p>
{{% /notice %}}
