---
title: "Corrective Change Exercise" 
chapter: true
weight: 40
---

# Unauthorized changes to sudo exercise

In this lab we'll enroll the additional EC2 instance you deployed while setting up prerequisites into Puppet Enterprise and start managing sudo. When sudo is managed we'll look at how our imported workflow is triggered then make a simple change to the EC2 instance to trigger a corrective change on the next Puppet run. With the sudo configuration successfully remediated, return to Relay one more time and observe the difference between this execution of our workflow vs. the previous envocation.

1. Navigate the **PE Agent** node group
![Step 1](/images/40_Exercise/01_pe_node_group_agent.png)

2. Add class **profile::base** 
![Step 2](/images/40_Exercise/02_pe_add_profile_base.png)

3. Commit chnages to **PE Agent** node group
![Step 3](/images/40_Exercise/03_pe_commit_profile_base.png)

4. Naviage to **Nodes** section via the vertical navigation bar
![Step 4](/images/40_Exercise/04_pe_nodes_section.png)

5. Click on the **Add nodes** button
![Step 5](/images/40_Exercise/05_pe_add_nodes.png)

6. Click on the **Install agents** button
![Step 6](/images/40_Exercise/06_pe_install_agents.png)

7. Copy command for initiating an agent install from the cli
![Step 7](/images/40_Exercise/07_pe_copy_installer_cmd.png)

8. Run copied command on EC2 instance
![Step 8](/images/40_Exercise/08_agent_cli_run_installer_cmd.png)

9. Run Puppet for the first time, waiting for onboarding approval
![Step 9](/images/40_Exercise/09_agent_cli_first_run_wait.png)

10. Navigate to **Certificates** section of PE console
![Step 10](/images/40_Exercise/10_pe_certificates_section.png)

11. Select **Unsigned Certificates** tab
![Step 11](/images/40_Exercise/11_pe_new_certificates_tab.png)

12. Accept new agent certificate
![Step 12](/images/40_Exercise/12_pe_accept_agent_cert.png)

13. Wait for Puppet to finish its initial run
![Step 13](/images/40_Exercise/13_agent_first_run_complete.png)

14. Switch to Relay to observe workflow trigger
![Step 14](/images/40_Exercise/14_relay_select_workflow.png)

15. Examine steps to see where workflow exits
![Step 15](/images/40_Exercise/15_relay_no_changes_run.png)

16. Verify that no changes were detected by examining step logs
![Step 16](/images/40_Exercise/16_relay_no_changes_log.png)

17. Make a change to the EC2 instance's sudo configuration out of band of Puppet
![Step 17](/images/40_Exercise/17_rm_sudo_run_puppet.png)

18. Re-run Puppet to trigger a corrective change
![Step 18](/images/40_Exercise/18_puppet_run_corrective.png)

19. Return to Relay again to witness the post corrective change workflow run
![Step 19](/images/40_Exercise/19_relay_changes_run.png)

20. Approve instance shutdown action
![Step 20](/images/40_Exercise/20_relay_approve_stop.png)

21. Once complete, verify which instance ID was shutdown by Relay
![Step 21](/images/40_Exercise/21_relay_stop_log.png)

22. Once shutdown, your SSH connection will also be terminated
![Step 22](/images/40_Exercise/22_puppet_cli_instances_stopped.png)

