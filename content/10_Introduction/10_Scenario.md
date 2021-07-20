---
title: "Scenario" 
chapter: true
weight: 11
---

## Going beyond simple management

### Premise

Your team has just completed automation for the deployment of your sudo configuration for your fleet of EC2 instances by bringing them under management with Puppet Enterprise. The automation of sudo is now so thorough that the organization has determined that any modification of its configurations outside of Puppet Enterprise should be considered a policy violation or potential, a security incident. Changes to this configurations must go through a proper review and an approval process, which is facilitated by the centrally managed repository of Puppet modules so any changes outside of this process are either an active breech or has the potential to cause one. 

While getting familiar with the reports available in the Puppet Enterprise console the team has come to appreciate the difference between changes that are reported as intentional and corrective. An intentional change being one you desire by newly defining it in Puppet Enterprise's central repository,  corrective changes being things that have unintentionally drifted from the state it was previously defined as in the central repository and then remediated back to compliance. Instead of reviewing these reports on a frequent basis to catch and take manual action upon any unauthorized changes to sudo configurations, you'd like to leverage these corrective events emitted by Puppet Enterprise to take immediate automated action to limit unintended damage.

After some research your team learns of Relay by Puppet, an easy workflow automation solution for cloud operations teams which can both integrate with Puppet Enterprise and AWS to take action upon these events and many more.